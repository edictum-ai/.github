<div align="center">

# Edictum

**Runtime contract enforcement for AI agent tool calls**

Deterministic YAML contracts that execute outside the model.<br>
Can't be prompt-injected. Fail-closed by default. 55us overhead.

[![PyPI](https://img.shields.io/pypi/v/edictum?label=PyPI&color=blue)](https://pypi.org/project/edictum/)
[![npm](https://img.shields.io/npm/v/edictum?label=npm&color=blue)](https://www.npmjs.com/package/edictum)
[![Go Reference](https://pkg.go.dev/badge/github.com/edictum-ai/edictum-go.svg)](https://pkg.go.dev/github.com/edictum-ai/edictum-go)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![arXiv](https://img.shields.io/badge/arXiv-2503.07918-b31b1b.svg)](https://arxiv.org/abs/2503.07918)
[![Docs](https://img.shields.io/badge/docs-edictum.ai-blue)](https://docs.edictum.ai)

</div>

---

## SDKs

| SDK | Install | Adapters |
|-----|---------|----------|
| [**Python**](https://github.com/edictum-ai/edictum) | `pip install edictum` | LangChain, CrewAI, Agno, Semantic Kernel, OpenAI Agents, Claude SDK, Nanobot, Google ADK |
| [**TypeScript**](https://github.com/edictum-ai/edictum-ts) | `npm install edictum` | Claude SDK, LangChain, OpenAI Agents, OpenClaw, Vercel AI |
| [**Go**](https://github.com/edictum-ai/edictum-go) | `go get github.com/edictum-ai/edictum-go` | ADK Go, Anthropic, Eino, Genkit, LangChain Go |

## Console

Self-hostable ops console for HITL approvals, audit feeds, and fleet monitoring.

```bash
docker pull ghcr.io/edictum-ai/edictum-console
```

[edictum-console](https://github.com/edictum-ai/edictum-console) -- all 3 SDKs connect via `edictum[server]`

## Gate

Governance for coding assistants (Claude Code, Cursor, Windsurf).

```bash
pip install edictum
```

[Learn more](https://docs.edictum.ai/gate)

## More

| Repo | What |
|------|------|
| [edictum-schemas](https://github.com/edictum-ai/edictum-schemas) | Contract bundle JSON Schema (single source of truth) |
| [edictum-demo](https://github.com/edictum-ai/edictum-demo) | Scenario demos, adversarial tests, benchmarks |

---

<div align="center">

[Website](https://edictum.ai) · [Docs](https://docs.edictum.ai) · [Research](https://arxiv.org/abs/2503.07918) · [PyPI](https://pypi.org/project/edictum/) · [npm](https://www.npmjs.com/package/edictum)

</div>
