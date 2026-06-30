<div align="center">

<img src="../assets/edictum-mark.svg" alt="" width="40">
<img src="../assets/captatum-mark.svg" alt="" width="40">
<img src="../assets/qratum-mark.svg" alt="" width="40">

# edictum-ai

A family of tools for AI agents in production — enforcement, fetch, and provenance.

[![PyPI](https://img.shields.io/pypi/v/edictum?label=PyPI&color=blue)](https://pypi.org/project/edictum/)
[![npm](https://img.shields.io/npm/v/@edictum/core?label=@edictum/core&color=blue)](https://www.npmjs.com/package/@edictum/core)
[![npm captatum](https://img.shields.io/npm/v/@edictum/captatum?label=@edictum/captatum&color=blue)](https://www.npmjs.com/package/@edictum/captatum)
[![Go Reference](https://pkg.go.dev/badge/github.com/edictum-ai/edictum-go.svg)](https://pkg.go.dev/github.com/edictum-ai/edictum-go)
[![Docs](https://img.shields.io/badge/docs-docs.edictum.ai-blue)](https://docs.edictum.ai)
[![Website](https://img.shields.io/badge/site-edictum.ai-black)](https://edictum.ai)
[![License: MIT](https://img.shields.io/badge/license-MIT-green)](https://opensource.org/licenses/MIT)

</div>

---

## Tools

| | Tool | Role | Install |
| --- | --- | --- | --- |
| <img src="../assets/edictum-mark.svg" width="14"> | [Edictum](https://github.com/edictum-ai/edictum) | Runtime enforcement for agent tool calls — rules and workflow gates at the tool boundary (Python / TypeScript / Go) | `pip install edictum[yaml]` · `pnpm add @edictum/core` · `go get github.com/edictum-ai/edictum-go` |
| <img src="../assets/captatum-mark.svg" width="14"> | [Captatum](https://github.com/edictum-ai/captatum) | Adaptive MCP web-fetch — fetch any URL, render JS when needed, return content plus a provenance receipt | `npx -y @edictum/captatum` |
| <img src="../assets/qratum-mark.svg" width="14"> | [Qratum](https://github.com/edictum-ai/qratum) | Session vault — capture, redact, and prove the provenance of agent runs | see [repo](https://github.com/edictum-ai/qratum) |

## Edictum SDKs

| Surface | Install | Notes |
| --- | --- | --- |
| [Python SDK](https://github.com/edictum-ai/edictum) | `pip install edictum[yaml]` | Reference SDK with 8 framework integrations |
| [TypeScript SDK](https://github.com/edictum-ai/edictum-ts) | `pnpm add @edictum/core @edictum/vercel-ai` | Core runtime plus adapter packages |
| [Go SDK](https://github.com/edictum-ai/edictum-go) | `go get github.com/edictum-ai/edictum-go` | Includes the `edictum gate` CLI |
| [OpenClaw integration](https://github.com/edictum-ai/edictum-openclaw) | `openclaw plugins install @edictum/edictum` | Native plugin plus manual adapter path |

## Repositories

| Repo | Role |
| --- | --- |
| [captatum](https://github.com/edictum-ai/captatum) | Adaptive MCP web-fetch |
| [edictum](https://github.com/edictum-ai/edictum) | Python SDK |
| [edictum-ts](https://github.com/edictum-ai/edictum-ts) | TypeScript SDK monorepo |
| [edictum-go](https://github.com/edictum-ai/edictum-go) | Go SDK and Gate CLI |
| [edictum-openclaw](https://github.com/edictum-ai/edictum-openclaw) | OpenClaw plugin and adapter |
| [edictum-schemas](https://github.com/edictum-ai/edictum-schemas) | Shared schemas and conformance fixtures |
| [edictum-demo](https://github.com/edictum-ai/edictum-demo) | Demo scenarios and example policies |
| [qratum](https://github.com/edictum-ai/qratum) | Session provenance vault |

Private server, website, and docs repos exist in the org, but they are not listed here because this profile is public.

## Research

- [Mind the GAP: Text Safety Does Not Transfer to Tool-Call Safety in LLM Agents](https://arxiv.org/abs/2602.16943)
- [Documentation](https://docs.edictum.ai)
- [Website](https://edictum.ai)

<div align="center">

[docs.edictum.ai](https://docs.edictum.ai) · [edictum.ai](https://edictum.ai) · [PyPI](https://pypi.org/project/edictum/) · [npm](https://www.npmjs.com/package/@edictum/core) · [Go pkg](https://pkg.go.dev/github.com/edictum-ai/edictum-go)

</div>
