# AI DLC

This repository is a library of reusable AI agents and skills. When this repo is added as context, use the index below to find and follow agent personas or skill procedures.

## Agents

When the user asks you to act as one of these agents, read the linked file and follow its instructions.

> **Recommended entry point:** Use the **Orchestrator** agent. It analyzes your prompt and delegates to the right specialist agent(s) automatically.

| Agent | File | Summary |
|-------|------|---------|
| **Orchestrator** | `agents/orchestrator.md` | **Entry point** — analyzes prompts, plans workflows, delegates to sub-agents |
| Architect | `agents/architect.md` | Proposes architecture options with trade-offs, records decisions as ADRs |
| Brainstormer | `agents/brainstormer.md` | Collaborative ideation partner, backs up answers with evidence |
| Designer | `agents/designer.md` | Creates app mockups and records design decisions |
| Developer | `agents/developer.md` | Implements features, fixes, and refactors based on user context |
| Explorer | `agents/explorer.md` | Read-only codebase exploration and Q&A |
| Product Owner | `agents/product-owner.md` | Generates features, user stories, and development tasks from project documents |

## Skills

When the user references a skill, read the linked file and follow its procedure.

| Skill | File | Agents | Summary |
|-------|------|--------|---------|
| Hello World | `skills/hello-world/README.md` | — | Example template for creating new skills |
| Plan | `skills/plan/README.md` | Product Owner, Orchestrator | Reads project context and generates a structured work plan for downstream agents |
| Code Review | `skills/code-review/README.md` | Developer, Architect, Explorer | Systematic code review with quality, security, and convention checks |
| Research | `skills/research/README.md` | Brainstormer, Architect, Designer | Structured technology and pattern research with evidence |
| Document | `skills/document/README.md` | Architect, Designer, Developer, Product Owner | Generate and update project documentation |
| ADR | `skills/adr/README.md` | Architect | Architecture Decision Record lifecycle management |
| Wireframe | `skills/wireframe/README.md` | Designer | Text-based wireframes and UI component specifications |
| Story Map | `skills/story-map/README.md` | Product Owner | User story mapping with personas, activities, and release slices |
| Dependency Map | `skills/dependency-map/README.md` | Explorer | Trace and map code dependencies and call chains |
| Scaffold | `skills/scaffold/README.md` | Developer | Generate boilerplate by discovering and replicating existing project patterns |
| Debug | `skills/debug/README.md` | Developer | Systematic hypothesis-driven debugging with root cause analysis |
| Test Gen | `skills/test-gen/README.md` | Developer | Generate test cases — happy paths, edge cases, error scenarios |
| Spike | `skills/spike/README.md` | Brainstormer, Architect | Time-boxed technical investigation with go/no-go verdict |
