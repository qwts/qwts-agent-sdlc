# qwts-agent-sdlc

The VS Code Copilot SDLC chain of the `qwts` fleet: seven custom agents and 29 slash-command prompts that interactively gather the requirements sections of the SDLC guides and hand off to one another, plus the Copilot instructions file that routes to them. It is the fleet's **AI primitives** capability. The guides themselves stay in [agent-sop](https://github.com/qwts/agent-sop); this repository holds only the chain that walks them.

Provenance: extracted from [qwts/agent-sop](https://github.com/qwts/agent-sop) at commit [ed5c5d8](https://github.com/qwts/agent-sop/tree/ed5c5d8) under the fleet split agreed in [#371](https://github.com/qwts/agent-sop/discussions/371) and [#372](https://github.com/qwts/agent-sop/discussions/372). The agents, prompts, and instructions keep the paths VS Code discovers them at; the usage guide moved from the repository root to [docs/usage.md](docs/usage.md).

## Install

1. Copy or symlink `.github/agents`, `.github/prompts`, and `.github/copilot-instructions.md` into the project you are planning. VS Code discovers custom agents and prompts at exactly those paths.
2. Check the SDLC guides out at `docs/` of that workspace. The agents and prompts name the guides by workspace path — [docs/01-requirements_gathering.md](https://github.com/qwts/agent-sop/blob/ed5c5d8/docs/01-requirements_gathering.md) and its siblings — and read them with the `read` tool, which resolves against the open workspace, not against a URL. Run the chain inside a clone of agent-sop, or symlink its docs folder into the workspace. The markdown links in the same files point at the pinned agent-sop revision for reading outside VS Code.
3. Open the Chat view, pick an agent from the dropdown or type a start command. The session flows, handoffs, and behaviors are in [docs/usage.md](docs/usage.md).

## Agents

| Agent | Purpose | Start |
| --- | --- | --- |
| [Requirements Gathering](.github/agents/requirements-gathering.agent.md) | Interactively gather application functionality and UX requirements (Section 1) | `/requirements-start` |
| [Deployment Strategy](.github/agents/deployment-strategy.agent.md) | Interactively gather deployment strategy and infrastructure requirements (Section 2) | `/deployment-start` |
| [Database & Data Management](.github/agents/database-data-management.agent.md) | Interactively gather database, caching, and messaging/integration requirements (Section 3) | `/database-start` |
| [Security & Compliance](.github/agents/security-compliance.agent.md) | Interactively gather security and compliance requirements (Section 4) | `/security-start` |
| [Performance & Monitoring](.github/agents/performance-monitoring.agent.md) | Interactively gather performance and monitoring requirements (Section 5) | `/performance-start` |
| [Additional Considerations](.github/agents/additional-considerations.agent.md) | Interactively gather additional considerations: third-party tools, risks, timeline (Section 6) | `/additional-start` |
| [Technology Selection](.github/agents/technology-selection.agent.md) | Guide through technology selection and proof of concept planning | handoff only |

Sections run in any order; each agent's handoff buttons chain to the others.

## Prompt commands

Type `/` in the Chat input to see them. Each prompt runs in the agent named in its front matter.

- [/requirements-start](.github/prompts/requirements-start.prompt.md) — Start interactive requirements gathering for Section 1 (Application Functionality and User Experience)
- [/requirements-core](.github/prompts/requirements-core.prompt.md) — Jump to Section 1.1 Core Features questions
- [/requirements-flows](.github/prompts/requirements-flows.prompt.md) — Jump to Section 1.2 User Flows questions
- [/requirements-ux](.github/prompts/requirements-ux.prompt.md) — Jump to Section 1.3 UX/UI Considerations questions
- [/requirements-summary](.github/prompts/requirements-summary.prompt.md) — Request a consolidated summary of requirements gathered so far
- [/deployment-start](.github/prompts/deployment-start.prompt.md) — Start interactive deployment strategy gathering for Section 2 (Environment Approach and Infrastructure/Scaling)
- [/deployment-env](.github/prompts/deployment-env.prompt.md) — Jump to Section 2.1 Environment Approach questions
- [/deployment-scaling](.github/prompts/deployment-scaling.prompt.md) — Jump to Section 2.2 Infrastructure and Scaling questions
- [/deployment-summary](.github/prompts/deployment-summary.prompt.md) — Request a consolidated summary of deployment strategy gathered so far
- [/database-start](.github/prompts/database-start.prompt.md) — Start interactive database and data management gathering for Section 3 (Database, Caching, Messaging)
- [/database-requirements](.github/prompts/database-requirements.prompt.md) — Jump to Section 3.1 Database Requirements questions
- [/database-caching](.github/prompts/database-caching.prompt.md) — Jump to Section 3.2 Caching questions
- [/database-messaging](.github/prompts/database-messaging.prompt.md) — Jump to Section 3.3 Messaging and Integration questions
- [/database-summary](.github/prompts/database-summary.prompt.md) — Request a consolidated summary of database and data management gathered so far
- [/security-start](.github/prompts/security-start.prompt.md) — Start interactive security and compliance gathering for Section 4 (Auth, Regulatory, Encryption)
- [/security-auth](.github/prompts/security-auth.prompt.md) — Jump to Section 4.1 Authentication and Authorization questions
- [/security-compliance](.github/prompts/security-compliance.prompt.md) — Jump to Section 4.2 Regulatory and Compliance questions
- [/security-encryption](.github/prompts/security-encryption.prompt.md) — Jump to Section 4.3 Data Encryption questions
- [/security-summary](.github/prompts/security-summary.prompt.md) — Request a consolidated summary of security and compliance gathered so far
- [/performance-start](.github/prompts/performance-start.prompt.md) — Start interactive performance and monitoring gathering for Section 5 (Response Times, Metrics, Alerting)
- [/performance-response-times](.github/prompts/performance-response-times.prompt.md) — Jump to Section 5.1 Response Times and Throughput questions
- [/performance-metrics](.github/prompts/performance-metrics.prompt.md) — Jump to Section 5.2 Metrics and Logs questions
- [/performance-alerting](.github/prompts/performance-alerting.prompt.md) — Jump to Section 5.3 Real-time Monitoring and Alerting questions
- [/performance-summary](.github/prompts/performance-summary.prompt.md) — Request a consolidated summary of performance and monitoring gathered so far
- [/additional-start](.github/prompts/additional-start.prompt.md) — Start interactive additional considerations gathering for Section 6 (Third-party, Risks, Timeline)
- [/additional-third-party](.github/prompts/additional-third-party.prompt.md) — Jump to Section 6.1 Third-party Tools and Services questions
- [/additional-risks](.github/prompts/additional-risks.prompt.md) — Jump to Section 6.2 Risks and Dependencies questions
- [/additional-timeline](.github/prompts/additional-timeline.prompt.md) — Jump to Section 6.3 Timeline and Deadlines questions
- [/additional-summary](.github/prompts/additional-summary.prompt.md) — Request a consolidated summary of additional considerations gathered so far

## Where the pin is recorded

The fleet loads this chain by SHA, never by branch. The pin lives in the `sdlc` capability entry of [qwts-agent-org](https://github.com/qwts/qwts-agent-org)'s `org.json`, not here. The guide links in the agents and prompts carry the agent-sop revision that entry pins — `ed5c5d8` at extraction time; when the org repo moves the pin, the links here are updated to match.

## Documentation

- [docs/usage.md](docs/usage.md) — the usage guide: each agent's session flow, key behaviors, handoffs, and the full command table.
- [AGENTS.md](AGENTS.md) — agent context for working in this repository.
- [.github/copilot-instructions.md](.github/copilot-instructions.md) — the Copilot adapter onto AGENTS.md, carrying the section-to-agent routing table.
- [ENG-0006](https://github.com/qwts/agent-sop/blob/main/docs/decisions/ENG-0006-agentic-primitives-governance.md) — the record governing agent primitives such as these; it stays in agent-sop.
