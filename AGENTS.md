# AGENTS.md

Canonical, vendor-neutral agent context for this repository, per [ENG-0006](https://github.com/qwts/agent-sop/blob/main/docs/decisions/ENG-0006-agentic-primitives-governance.md). [.github/copilot-instructions.md](.github/copilot-instructions.md) is the Copilot adapter onto this file: it adds Copilot-specific orientation and never restates what is here.

## What this repository is

The `qwts` fleet's AI-primitives capability: the VS Code Copilot SDLC chain (custom agents, prompts, and the Copilot instructions file) extracted from agent-sop. Map, install steps, and the agent and command tables: [README.md](README.md).

## Shared agent conventions

PR-first workflow, validation before push, commit and PR hygiene, and the untrusted-input threat model are defined once, for every repo, in the [org-wide agent conventions](https://github.com/qwts/agent-sop/blob/main/docs/reference/agent-conventions.md). This repository is governed by [agent-sop](https://github.com/qwts/agent-sop): its [shared SOPs](https://github.com/qwts/agent-sop/blob/main/docs/sop/README.md) and [engineering decisions](https://github.com/qwts/agent-sop/blob/main/docs/decisions/README.md) apply here by default ([ENG-0008](https://github.com/qwts/agent-sop/blob/main/docs/decisions/ENG-0008-shared-sop-inheritance.md): inherit by default, vary by explicit delta).

## What is specific to this repository

- **Every file under `.github/agents`, `.github/prompts`, and `.github/copilot-instructions.md` is an ENG-0006 primitive.** Agents read it as directives, so it changes through PR review only, and the PR states what agent behavior changes.
- **The guides live in agent-sop, not here.** Links to them are pinned to the agent-sop commit that the `sdlc` capability in qwts-agent-org's `org.json` records (ed5c5d8 at extraction). Do not repoint them at `main` and do not copy guide content in; the chain reads the guides as workspace files at `docs/`, as the README's install section explains.
- **Gates before a PR:** `npm run lint:markdown`, and the docs-gov gate against `docs-gov.config.json` using the docs-gov engine from its home checkout (`node <engine>/docs-gov.mjs --root <this checkout>`). CI runs the markdownlint gate. New markdown must be reachable by link from [README.md](README.md) or the `orphan-doc` rule fails it. Handoff entries in agent front matter are identical across agents by design, so the config's duplicate-statement allowance exempts blocks containing `send: false`.
