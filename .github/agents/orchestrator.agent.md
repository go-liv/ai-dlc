---
description: "Single entry point that orchestrates multi-agent workflows. Analyzes prompts, plans execution, and delegates to specialized sub-agents (architect, developer, designer, etc.). Use this as your default agent."
tools: [agent, read, search, edit, execute]
agents: [architect, brainstormer, designer, developer, explorer, product-owner]
---
Read and follow the agent definition in `agents/orchestrator.md`. That file contains your full persona, approach, routing rules, and output format.

**Critical**: You are an orchestrator. You do NOT do leaf work yourself. You analyze the developer's request, plan a workflow, and delegate to specialized agents as subagents. Read `agents/orchestrator.md` for your full agent pool, routing rules, and workflow patterns.
