<p align="center">
  <a href="https://edictum.ai">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/edictum-ai/.github/main/assets/shield-dark.svg" width="72">
      <img src="https://raw.githubusercontent.com/edictum-ai/.github/main/assets/shield-light.svg" width="72" alt="Edictum">
    </picture>
  </a>
</p>

<h3 align="center">Runtime contract enforcement for AI agent tool calls</h3>

<p align="center">
  Deterministic YAML contracts that execute outside the model.<br>
  Can't be prompt-injected. Fail-closed by default.
</p>

<p align="center">
  <a href="https://pypi.org/project/edictum/"><img src="https://img.shields.io/pypi/v/edictum?color=F59E0B&label=PyPI" alt="PyPI"></a>&nbsp;
  <a href="https://github.com/edictum-ai/edictum/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-F59E0B" alt="MIT License"></a>&nbsp;
  <a href="https://arxiv.org/abs/2602.16943"><img src="https://img.shields.io/badge/arXiv-2602.16943-b31b1b" alt="arXiv"></a>&nbsp;
  <a href="https://docs.edictum.ai"><img src="https://img.shields.io/badge/docs-edictum.ai-475569" alt="Docs"></a>
</p>

---

### [`edictum`](https://github.com/edictum-ai/edictum) — Core Library

YAML contracts govern what agents do with tools — before the call executes. 8 framework adapters. Zero dependencies. ~55µs overhead.

```
pip install edictum
```

### [`edictum-console`](https://github.com/edictum-ai/edictum-console) — Operations Console

Self-hosted management plane. Fleet monitoring · HITL approvals · hot-reload contracts · audit feeds · Slack / Telegram / Discord.

```
docker pull ghcr.io/edictum-ai/edictum-console:latest
```

### Edictum Gate — Coding Assistant Governance

Pre-execution contracts for Claude Code, Cursor, Copilot CLI. Every tool call evaluated before it runs.

```
pip install edictum[gate]
```

---

<p align="center">
  <a href="https://edictum.ai">Website</a>&nbsp;&nbsp;·&nbsp;&nbsp;<a href="https://docs.edictum.ai">Docs</a>&nbsp;&nbsp;·&nbsp;&nbsp;<a href="https://arxiv.org/abs/2602.16943">Research — arXiv:2602.16943</a>&nbsp;&nbsp;·&nbsp;&nbsp;<a href="https://pypi.org/project/edictum/">PyPI</a>
</p>
