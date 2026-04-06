<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="../assets/shield-dark.svg">
  <img src="../assets/shield-light.svg" alt="Edictum shield" width="96" height="96">
</picture>

# Edictum

Runtime enforcement for AI agent tool calls.

Write rules and workflows in YAML. Enforce them at the tool boundary across Python, TypeScript, Go, and OpenClaw.

[![PyPI](https://img.shields.io/pypi/v/edictum?label=PyPI&color=blue)](https://pypi.org/project/edictum/)
[![npm](https://img.shields.io/npm/v/@edictum/core?label=npm&color=blue)](https://www.npmjs.com/package/@edictum/core)
[![Go Reference](https://pkg.go.dev/badge/github.com/edictum-ai/edictum-go.svg)](https://pkg.go.dev/github.com/edictum-ai/edictum-go)
[![Docs](https://img.shields.io/badge/docs-docs.edictum.ai-blue)](https://docs.edictum.ai)
[![Website](https://img.shields.io/badge/site-edictum.ai-black)](https://edictum.ai)
[![License: MIT](https://img.shields.io/badge/license-MIT-green)](https://opensource.org/licenses/MIT)

</div>

---

## What Ships

- Rulesets: deterministic pre, post, session, and sandbox checks for tool calls
- Workflow Gates: stateful process enforcement for coding-agent flows
- Server-backed enforcement: approvals, audit feeds, remote rulesets, and hot reload
- 18 shipped integrations across the ecosystem: 8 Python, 5 TypeScript, 5 Go

## Start Here

| Surface | Install | Notes |
| --- | --- | --- |
| [Python SDK](https://github.com/edictum-ai/edictum) | `pip install edictum[yaml]` | Reference SDK with 8 framework integrations |
| [TypeScript SDK](https://github.com/edictum-ai/edictum-ts) | `pnpm add @edictum/core @edictum/vercel-ai` | Core runtime plus adapter packages |
| [Go SDK](https://github.com/edictum-ai/edictum-go) | `go get github.com/edictum-ai/edictum-go` | Includes the `edictum gate` CLI |
| [OpenClaw integration](https://github.com/edictum-ai/edictum-openclaw) | `openclaw plugins install @edictum/edictum` | Native plugin plus manual adapter path |

## Repositories

| Repo | Role |
| --- | --- |
| [edictum](https://github.com/edictum-ai/edictum) | Python SDK |
| [edictum-ts](https://github.com/edictum-ai/edictum-ts) | TypeScript SDK monorepo |
| [edictum-go](https://github.com/edictum-ai/edictum-go) | Go SDK and Gate CLI |
| [edictum-openclaw](https://github.com/edictum-ai/edictum-openclaw) | OpenClaw plugin and adapter |
| [edictum-api](https://github.com/edictum-ai/edictum-api) | Server API for approvals, audit, and remote policy |
| [edictum-hub](https://github.com/edictum-ai/edictum-hub) | Website and dashboard surface |
| [edictum-docs](https://github.com/edictum-ai/edictum-docs) | Documentation site |
| [edictum-schemas](https://github.com/edictum-ai/edictum-schemas) | Shared schemas and conformance fixtures |
| [edictum-demo](https://github.com/edictum-ai/edictum-demo) | Demo scenarios and example policies |

## Research

- [Runtime Contract Enforcement for AI Agents](https://arxiv.org/abs/2602.16943)
- [Documentation](https://docs.edictum.ai)
- [Website](https://edictum.ai)

<div align="center">

[docs.edictum.ai](https://docs.edictum.ai) · [edictum.ai](https://edictum.ai) · [PyPI](https://pypi.org/project/edictum/) · [npm](https://www.npmjs.com/package/@edictum/core) · [Go pkg](https://pkg.go.dev/github.com/edictum-ai/edictum-go)

</div>
