# Self-Hosted GitHub Actions Runner

## Overview

The `edictum-ai` organization uses an org-level self-hosted runner shared across all repositories. The runner operates in **ephemeral mode**, guaranteeing a clean state after every job — no artifacts, credentials, or build outputs persist between runs.

- **Host:** Dedicated Mac Mini (ARM64, macOS)
- **Mode:** Ephemeral — deregisters after each job, re-registers with a fresh token
- **Work directory:** `/tmp/gh-runner-work` (cleaned on reboot and between jobs)
- **Scope:** Organization-level — available to all `edictum-ai/*` repos

---

## Hardware Requirements

| Component | Minimum | Notes |
|-----------|---------|-------|
| Machine | Mac Mini M-series | ARM64 architecture required |
| OS | macOS 14+ (Sonoma) | Apple Silicon native |
| RAM | 16 GB | Claude review workflows use ~4 GB |
| Storage | 256 GB SSD | Ephemeral work dir keeps disk usage low |
| Network | Always-on connection | Outbound HTTPS to GitHub and package registries |

---

## Software Prerequisites

Install the following before configuring the runner:

```bash
# Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Python 3.11+ (via pyenv or homebrew)
brew install pyenv
pyenv install 3.11
pyenv global 3.11

# Node.js 22+ (via nvm or homebrew)
brew install nvm
nvm install 22
nvm use 22

# Go 1.25+
brew install go

# pnpm
npm install -g pnpm

# uv (Python package installer)
pip install uv

# GitHub CLI (must be authenticated)
brew install gh
gh auth login

# Docker (for edictum-console builds)
brew install --cask docker
```

Verify all tools are available:

```bash
python3 --version   # 3.11+
node --version       # 22+
go version           # 1.25+
pnpm --version
uv --version
gh --version
docker --version
```

---

## Installation

Download and extract the runner:

```bash
mkdir ~/actions-runner && cd ~/actions-runner

curl -o actions-runner-osx-arm64-2.333.0.tar.gz -L \
  https://github.com/actions/runner/releases/download/v2.333.0/actions-runner-osx-arm64-2.333.0.tar.gz

echo "d92ea082bede9616120800b0e4a09f1aa209c922ade05d59bc3ee7c4de56f73c  actions-runner-osx-arm64-2.333.0.tar.gz" | shasum -a 256 -c

tar xzf ./actions-runner-osx-arm64-2.333.0.tar.gz
```

> **Always verify the checksum.** If it fails, re-download or check for a newer release at [actions/runner releases](https://github.com/actions/runner/releases).

---

## Configuration (Hardened)

Register the runner at the organization level with ephemeral mode and an isolated work directory:

```bash
# Generate a one-time registration token via the GitHub API
TOKEN=$(gh api orgs/edictum-ai/actions/runners/registration-token -X POST --jq '.token')

./config.sh \
  --url https://github.com/edictum-ai \
  --token "$TOKEN" \
  --name edictum-runner \
  --labels self-hosted,macOS,ARM64 \
  --work /tmp/gh-runner-work \
  --ephemeral \
  --unattended
```

**Flags explained:**

| Flag | Purpose |
|------|---------|
| `--ephemeral` | Deregisters after one job — forces clean state |
| `--work /tmp/gh-runner-work` | Isolates build artifacts outside of user home |
| `--unattended` | No interactive prompts — suitable for automation |
| `--labels` | Makes the runner targetable in workflow `runs-on` |

---

## Running

### Manual start

```bash
cd ~/actions-runner
./run.sh
```

The runner picks up one job, executes it, then exits (ephemeral mode).

### Automated run loop

Use the following script to keep the runner alive across jobs. Save it as `~/actions-runner/run-loop.sh`:

```bash
#!/usr/bin/env bash
set -euo pipefail

RUNNER_DIR="$HOME/actions-runner"
WORK_DIR="/tmp/gh-runner-work"
ORG="edictum-ai"

log() { echo "[$(date '+%Y-%m-%d %H:%M:%S')] $*"; }

cleanup_work_dir() {
  if [[ -d "$WORK_DIR" ]]; then
    log "Cleaning work directory..."
    rm -rf "${WORK_DIR:?}"/*
  fi
  mkdir -p "$WORK_DIR"
}

register_runner() {
  log "Fetching registration token..."
  local token
  token=$(gh api "orgs/${ORG}/actions/runners/registration-token" -X POST --jq '.token')

  log "Registering runner (ephemeral)..."
  "$RUNNER_DIR/config.sh" \
    --url "https://github.com/${ORG}" \
    --token "$token" \
    --name edictum-runner \
    --labels self-hosted,macOS,ARM64 \
    --work "$WORK_DIR" \
    --ephemeral \
    --unattended \
    --replace
}

main() {
  while true; do
    cleanup_work_dir
    register_runner

    log "Starting runner..."
    "$RUNNER_DIR/run.sh" || log "Runner exited with code $?"

    log "Job complete. Re-registering for next job..."
    sleep 2
  done
}

main
```

```bash
chmod +x ~/actions-runner/run-loop.sh
```

---

## Security Hardening

### Ephemeral mode (enforced)

Every job runs on a freshly registered runner instance. After the job completes, the runner deregisters — no state, credentials, or artifacts carry over.

### Isolated work directory

Build artifacts go to `/tmp/gh-runner-work`, not the user's home directory. The `run-loop.sh` script wipes this directory between every job.

### Workflow tool restrictions

Claude-powered review workflows restrict available tools to read-only operations:

- `git diff`
- `cat` / `Read`
- `Glob`
- `Grep`

**No arbitrary shell execution** is permitted in review workflows.

### Recommended hardening

| Measure | Why |
|---------|-----|
| **Dedicated macOS user account** | Run the runner under a non-admin user (e.g., `_ghrunner`) to limit blast radius |
| **FileVault encryption** | Encrypts disk at rest — protects secrets if hardware is stolen |
| **Firewall (outbound HTTPS only)** | Block inbound connections; only allow outbound to GitHub, npm, PyPI, Docker Hub |
| **Disable remote login** | SSH/VNC should be off unless actively needed for maintenance |

---

## Maintenance

### Runner updates

GitHub notifies when a new runner version is available. To check manually:

```bash
cd ~/actions-runner
./config.sh --check
```

To update, download the new release tarball and re-extract over the existing directory.

### Token rotation

Tokens are inherently short-lived in ephemeral mode — each registration uses a one-time token that expires after the job completes. No manual rotation needed.

### Logs and diagnostics

Runner logs are stored in:

```
~/actions-runner/_diag/
```

Check these logs when jobs fail unexpectedly or the runner fails to register.

### Reboot recovery

The runner auto-starts on boot via the launchd service described below.

---

## launchd Service (Auto-Start on Boot)

Create the following plist to start the runner automatically on boot.

Save as `/Library/LaunchDaemons/com.edictum.actions-runner.plist`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.edictum.actions-runner</string>

    <key>ProgramArguments</key>
    <array>
        <string>/bin/bash</string>
        <string>/Users/ghrunner/actions-runner/run-loop.sh</string>
    </array>

    <key>UserName</key>
    <string>ghrunner</string>

    <key>WorkingDirectory</key>
    <string>/Users/ghrunner/actions-runner</string>

    <key>RunAtLoad</key>
    <true/>

    <key>KeepAlive</key>
    <true/>

    <key>StandardOutPath</key>
    <string>/Users/ghrunner/actions-runner/_diag/launchd-stdout.log</string>

    <key>StandardErrorPath</key>
    <string>/Users/ghrunner/actions-runner/_diag/launchd-stderr.log</string>

    <key>EnvironmentVariables</key>
    <dict>
        <key>PATH</key>
        <string>/opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin</string>
        <key>HOME</key>
        <string>/Users/ghrunner</string>
    </dict>
</dict>
</plist>
```

Install and start the service:

```bash
# Copy plist (requires admin)
sudo cp com.edictum.actions-runner.plist /Library/LaunchDaemons/

# Set ownership
sudo chown root:wheel /Library/LaunchDaemons/com.edictum.actions-runner.plist

# Load and start
sudo launchctl load /Library/LaunchDaemons/com.edictum.actions-runner.plist
```

> **Note:** Adjust `UserName` and paths if you're not using a dedicated `ghrunner` account. The `PATH` must include Homebrew's bin directory for `gh`, `node`, `python3`, etc. to be found.

To stop and unload:

```bash
sudo launchctl unload /Library/LaunchDaemons/com.edictum.actions-runner.plist
```

---

## Targeting the Runner in Workflows

Use the runner's labels in your workflow files:

```yaml
jobs:
  review:
    runs-on: [self-hosted, macOS, ARM64]
    steps:
      - uses: actions/checkout@v4
      # ...
```
