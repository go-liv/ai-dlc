# AI DLC — Project Instructions

This repository is a library of reusable AI agents and skills. When this repo is added as context or as a workspace folder, use the index below to find and follow agent personas or skill procedures.

## Agents

Agents are personas with defined roles, constraints, and output formats. When the user asks you to act as one of these agents, read the linked file and follow its instructions.

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

Skills are step-by-step procedures for specific tasks. When the user references a skill, read the linked file and follow its procedure.

| Skill | File | Summary |
|-------|------|---------|
| Hello World | `skills/hello-world/README.md` | Example template for creating new skills |
| Plan | `skills/plan/README.md` | Reads project context and generates a structured work plan for downstream agents |
