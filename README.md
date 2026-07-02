# NovAiOS — Agent Operating System

**A modular operating system for multi-agent software production.**

> 🔒 **Closed-source, commercial system.** This repository is the public architecture tour.
> Live walkthrough & demo: [muratsuer.eu](https://muratsuer.eu) · Contact: murat@muratsuer.eu

---

## What it is

NovAiOS is an operating-system layer for AI coding agents. It sits between the agent host (e.g. Claude Code or any MCP-capable client) and the project, and gives agents what an OS gives processes: **memory, scheduling, permissions, tooling and audit**.

Agents running on NovAiOS plan, build, audit and ship complex software end to end — driven by an agentic project-management pipeline with quality gates, persistent multi-layer memory and integrated code intelligence.

## Architecture

```mermaid
flowchart TB
    subgraph HOST["Agent Host (Claude Code · any MCP client)"]
        H1["MCP surface + hooks"]
    end

    subgraph ADAPT["Host Adapters"]
        A1["Standardized HostAdapter protocol —\ncore is host-agnostic, branches on capability"]
    end

    subgraph CORE["NovAiOS Core"]
        direction TB
        K["Kernel\ncode intelligence · config · context assembly · contracts · observability"]
        F["Framework Engine\nstage-gated SOP pipelines · entry gates · Ed25519 licensing"]
        O["Orchestration\nsubagent dispatch · scratch stores · progress views"]
        M["Memory\n8-layer, DB-first · salience policy · turn capture · compaction"]
        E["Eval Harness\nmulti-agent memory integrity · secret-leak audit · thresholds · proof reports"]
        MCP["MCP Core (zero-dependency)\nmicrokernel · registry · stdio transport · token budget · security"]
    end

    subgraph STORE["Storage"]
        S1["SQLite (atomic writes, project catalog, key vault)"]
    end

    HOST --> ADAPT --> CORE --> STORE
```

## Subsystems

| Subsystem | What it does |
|---|---|
| **8-layer memory** | DB-first persistent memory: turn capture → summarization → compaction → long-term/procedural/wiki stores, with salience policy and project scoping |
| **Framework engine** | Declarative, stage-gated process frameworks (SOPs) that drive multi-subagent production; declaration gates block unverified "done" claims; Ed25519-signed licensing |
| **Code intelligence** | Built-in static-analysis engine: Tree-sitter AST → knowledge graph (entities, call/inheritance/data-flow edges), incremental updates via git hooks, exposed as token-budgeted MCP tools |
| **MCP core** | Own zero-dependency MCP server microkernel — registry, stdio transport, per-tool token budgets, security layer, stderr logging. 98% test coverage |
| **Eval harness** | Hermetic evaluation runs: multi-agent memory-isolation measurement, flat-context proofs, secret-leak audits, threshold-gated reports |
| **Orchestration** | Orchestrator + fresh-subagent dispatch with quality gates between stages — no context bleed between agents |
| **Security layer** | Dependency/CVE, secrets, IaC and taint analysis passes over project code, wired into the pipeline as gates |

## Design principles

- **Supply-chain-immune & air-gappable.** The core is Python-stdlib-only; optional layers are vendored and hash-locked. No live package pulls, ever.
- **Host-agnostic.** Every host connects through the same `HostAdapter` protocol; the core never branches on host name, only on declared capability.
- **Compliance-first.** Every agent action is captured, auditable and replayable; gates produce evidence, not vibes.
- **Token-budget enforcement.** Every MCP tool response is budget-capped so agents get minimal, precise context.

## By the numbers

- **490+** source modules · **3,800+** test functions
- **98%** coverage on the MCP core
- **12-language** code-intelligence engine ([architecture tour](https://github.com/murat-suer/code-intelligence))
- Dogfooded daily: NovAiOS builds and audits itself

## Stack

Python (stdlib-only core) · SQLite · MCP · Tree-sitter (vendored) · Ed25519 · Redis Streams (optional) · FastAPI (optional)

---

**Author:** [Murat Süer](https://muratsuer.eu) — AI Engineer & Data Scientist · [LinkedIn](https://linkedin.com/in/murat-suer)
*Source access and live demos available for interviews and evaluation.*
