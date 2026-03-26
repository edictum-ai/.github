<div align="center">

# Edictum

### Prompts are suggestions. Contracts are enforcement.

Runtime contract enforcement for AI agent tool calls.<br>
Deterministic YAML contracts that execute outside the model — can't be prompt-injected, fail-closed by default.

**3 SDKs** · **18 Adapters** · **55µs overhead** · **Zero runtime deps** · **Fail-closed**

[![PyPI](https://img.shields.io/pypi/v/edictum?label=PyPI&color=blue)](https://pypi.org/project/edictum/)
[![npm](https://img.shields.io/npm/v/@edictum/core?label=npm&color=blue)](https://www.npmjs.com/package/@edictum/core)
[![Go Reference](https://pkg.go.dev/badge/github.com/edictum-ai/edictum-go.svg)](https://pkg.go.dev/github.com/edictum-ai/edictum-go)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![arXiv](https://img.shields.io/badge/arXiv-2602.16943-b31b1b.svg)](https://arxiv.org/abs/2602.16943)
[![Docs](https://img.shields.io/badge/docs-edictum.ai-blue)](https://docs.edictum.ai)

</div>

---

## SDKs

| SDK | Install | Adapters |
|-----|---------|----------|
| [**Python**](https://github.com/edictum-ai/edictum) | `pip install edictum` | LangChain, CrewAI, Agno, Semantic Kernel, OpenAI Agents, Claude SDK, Nanobot, Google ADK |
| [**TypeScript**](https://github.com/edictum-ai/edictum-ts) | `npm install edictum` | Claude SDK, LangChain, OpenAI Agents, OpenClaw, Vercel AI |
| [**Go**](https://github.com/edictum-ai/edictum-go) | `go get github.com/edictum-ai/edictum-go` | ADK Go, Anthropic, Eino, Genkit, LangChain Go |

---

## OpenClaw Integration

> **Native plugin for [OpenClaw](https://github.com/openclaw/openclaw) (322K+ GitHub stars)**

```bash
openclaw plugins install @edictum/openclaw
```

One command. Zero config. Ships with a **770-line governance bundle** that enforces security contracts on every tool call — file access, network requests, shell commands, secrets handling, and more.

**Why this matters:** We scanned OpenClaw's 36K-skill public registry and **found live C2 malware**. Skills run arbitrary code with your agent's permissions. Edictum enforces contracts so a compromised skill can't exfiltrate data, pivot laterally, or phone home.

Two modes:
- **Standalone** — bundled contracts, zero config, works out of the box
- **Console-connected** — hot-reload contracts, fleet monitoring, HITL approvals via [Edictum Console](#console)

[`@edictum/openclaw` on npm](https://www.npmjs.com/package/@edictum/openclaw) · [Source](https://github.com/edictum-ai/edictum-openclaw)

---

## Console

Self-hostable ops console for HITL approvals, audit feeds, and fleet monitoring.

```bash
docker pull ghcr.io/edictum-ai/edictum-console
```

All 3 SDKs connect via `edictum[server]`. Single Docker image — deploy anywhere.

[edictum-console](https://github.com/edictum-ai/edictum-console)

## Gate

Governance for coding assistants (Claude Code, Cursor, Windsurf).

```bash
pip install edictum
```

[Learn more](https://docs.edictum.ai/gate)

## Research

- **arXiv paper:** [2602.16943 — Runtime Contract Enforcement for AI Agents](https://arxiv.org/abs/2602.16943)
- **OpenClaw registry scan:** Found live C2 malware in 36K public skills — contracts would have blocked every payload

---

## All Repos

| Repo | What |
|------|------|
| [edictum](https://github.com/edictum-ai/edictum) | Python SDK — reference implementation, 8 adapters |
| [edictum-ts](https://github.com/edictum-ai/edictum-ts) | TypeScript SDK — monorepo, 5 adapters |
| [edictum-go](https://github.com/edictum-ai/edictum-go) | Go SDK — full port, 5 adapters |
| [edictum-console](https://github.com/edictum-ai/edictum-console) | Ops console — HITL approvals, audit feeds, fleet monitoring |
| [edictum-openclaw](https://github.com/edictum-ai/edictum-openclaw) | Native OpenClaw plugin — 770-line governance bundle |
| [edictum-schemas](https://github.com/edictum-ai/edictum-schemas) | Contract bundle JSON Schema (single source of truth) |
| [edictum-demo](https://github.com/edictum-ai/edictum-demo) | Scenario demos, adversarial tests, benchmarks |

---

<div align="center">

[Website](https://edictum.ai) · [Docs](https://docs.edictum.ai) · [Research](https://arxiv.org/abs/2602.16943) · [PyPI](https://pypi.org/project/edictum/) · [npm](https://www.npmjs.com/package/@edictum/core)

</div>
