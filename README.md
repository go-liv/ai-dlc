# AI DLC

A library of reusable AI agents and skills. Works across VS Code Copilot, Cursor, and Claude.

> **Start here:** Use the **Orchestrator** agent. It analyzes your prompt and automatically delegates to the right specialist agent(s). You never need to pick a leaf agent yourself.

## Setup

### VS Code Copilot

1. Clone this repo
2. `File > Add Folder to Workspace...` → select the `ai-dlc` folder
3. Open Copilot Chat → click the **agent picker** dropdown → select **orchestrator**
4. Type your prompt — the orchestrator analyzes it and delegates to the right sub-agent(s)

> This is the most seamless experience: the orchestrator's `agents` frontmatter declares which sub-agents it can invoke, and the `agent` tool enables native subagent dispatch. Sub-agents are hidden from the picker (`user-invocable: false`) since they're meant to be invoked by the orchestrator.

### Cursor (prompt-driven)

Cursor doesn't have a native agent picker. The LLM follows agent/skill instructions when you reference them.

**Option A — Docs index (no clone):**
1. Go to **Cursor Settings > Features > Docs**
2. Add this repo's GitHub URL
3. In chat, type `@Docs` to pull in the repo as context
4. Say "act as the orchestrator agent" — it will delegate to specialists automatically

**Option B — Workspace folder:**
1. Clone this repo
2. Add it as a workspace folder
3. Cursor auto-reads `.cursorrules`, which indexes all agents and skills
4. Say "act as the orchestrator agent" or reference any agent by name

### Claude (prompt-driven)

Claude doesn't have a native agent picker. The LLM follows agent/skill instructions when you reference them.

**Claude Projects (web, no clone):**
1. Create or open a Project on claude.ai
2. In Project Knowledge, add this repo's GitHub URL or upload the files
3. Claude reads `CLAUDE.md` as the index
4. Say "act as the orchestrator agent" — it will delegate to specialists automatically

**Claude Code (CLI):**
1. Clone this repo into or alongside your project
2. Claude Code auto-reads `CLAUDE.md`
3. Say "act as the orchestrator agent" or reference any agent by name

### Platform Comparison

| Feature | VS Code Copilot | Cursor | Claude |
|---------|-----------------|--------|--------|
| Agent picker UI | Yes | No | No |
| Multi-agent orchestration | Native (subagents via `agents` frontmatter) | Simulated (persona switching) | Simulated (persona switching) |
| Skill auto-routing | Yes | No | No |
| Prompt-driven agents | Yes | Yes | Yes |
| Clone required | Yes | No | No* |

\* Claude Projects can index a GitHub URL directly; Claude Code requires a clone.

## Usage Examples

### VS Code Copilot (workspace folder — native)

The orchestrator is the recommended entry point. It natively delegates to specialist sub-agents.

**Using the orchestrator (recommended):**
1. Open Copilot Chat
2. Click the agent picker → select **orchestrator**
3. Type your prompt — it analyzes, plans, and delegates automatically

> *[Select `orchestrator` from picker]*
> "Build a REST API for user management with JWT auth"
>
> The orchestrator plans a workflow: Explorer → Architect → Developer, invoking each as isolated subagents.

> **Note:** Sub-agents are set to `user-invocable: false` and won't appear in the agent picker. They are only accessible through the orchestrator.

**Invoking a skill directly (slash command):**
> Type `/hello-world` in chat to invoke the skill by name.

---

### Cursor

The orchestrator works via persona switching — it reads each agent's definition and adopts it for that phase.

**Using the orchestrator (recommended):**
> "Act as the orchestrator agent. Build a REST API for user management with JWT auth."
>
> The orchestrator reads each needed agent's definition, delegates tasks sequentially, and synthesizes the result.

**Using a single agent directly:**
> "Act as the architect agent. I'm building a real-time notification system and need to choose between WebSockets, SSE, and polling."

**Using a skill:**
> "Follow the hello-world skill from ai-dlc to verify the setup is working."

**Combining agent + skill:**
> "Act as the developer agent. Use the hello-world skill to scaffold something and verify my DLC setup."

---

### Claude

The orchestrator works via persona switching — it reads each agent's definition and adopts it for that phase.

**Using the orchestrator (recommended):**
> "Act as the orchestrator agent. I want to add a dashboard to the app but I'm not sure what to show."
>
> The orchestrator chains: Brainstormer → Designer → Architect → Developer, switching personas at each step.

**Using a single agent directly:**
> "Act as the explorer agent. Find all the places where we handle authentication errors and summarize the patterns used."

**Using a skill:**
> "Follow the hello-world skill procedure to verify this DLC repo is accessible."

**Combining agent + context:**
> "Act as the architect agent. Look at the files in `src/services/` and propose options for breaking the payment service into its own module."

## How It Works

```
ai-dlc/
├── agents/                          # Canonical agent definitions (any LLM)
│   ├── orchestrator.md              # ★ Entry point — delegates to sub-agents
│   ├── architect.md
│   ├── brainstormer.md
│   ├── designer.md
│   ├── developer.md
│   ├── explorer.md
│   └── product-owner.md
├── skills/                          # Canonical skill definitions (any LLM)
│   ├── hello-world/
│   │   └── README.md
│   └── plan/
│       └── README.md
├── .github/
│   ├── copilot-instructions.md      # Copilot: workspace instructions (index)
│   ├── agents/                      # Copilot: native agent definitions
│   │   ├── orchestrator.agent.md    # ★ Copilot orchestrator (declares subagents)
│   │   ├── architect.agent.md       # user-invocable: false (subagent only)
│   │   ├── brainstormer.agent.md
│   │   ├── designer.agent.md
│   │   ├── developer.agent.md
│   │   ├── explorer.agent.md
│   │   └── product-owner.agent.md
│   └── skills/                      # Copilot: native skill auto-routing
│       ├── hello-world/
│       │   └── SKILL.md
│       └── plan/
│           └── SKILL.md
├── .cursorrules                     # Cursor entry point
└── CLAUDE.md                        # Claude entry point
```

- **`agents/`** and **`skills/`** are the canonical source — plain markdown, readable by any LLM on any platform.
- **`.github/agents/`** and **`.github/skills/`** are thin Copilot-native wrappers (frontmatter + reference to canonical file) that enable the agent picker and skill auto-routing.
- **`.cursorrules`** and **`CLAUDE.md`** are platform entry points that index the canonical files.

## Agents

| Agent | Description |
|-------|-------------|
| **[orchestrator](agents/orchestrator.md)** | **Entry point** — analyzes prompts, plans workflows, delegates to sub-agents |
| [architect](agents/architect.md) | Proposes architecture options with trade-offs, records decisions as ADRs |
| [brainstormer](agents/brainstormer.md) | Collaborative ideation partner, backs up answers with evidence |
| [designer](agents/designer.md) | Creates app mockups and records design decisions |
| [developer](agents/developer.md) | Implements features, fixes, and refactors based on user context |
| [explorer](agents/explorer.md) | Read-only codebase exploration and Q&A |
| [product-owner](agents/product-owner.md) | Generates features, user stories, and development tasks from project documents |

## Skills

| Skill | Description |
|-------|-------------|
| [hello-world](skills/hello-world/README.md) | Example template for creating new skills |
| [plan](skills/plan/README.md) | Reads project context and generates a structured work plan |

## Adding an Agent

Create a markdown file in `agents/` named `<name>.md`:

```markdown
# Agent Name

**Type:** Agent
**Tools:** read, search

## Description
What this agent does and when to use it.

## Persona
Who the agent is and what its purpose is.

## Constraints
- What it must NOT do

## Approach
1. Step-by-step method

## Output Format
What the agent returns.
```

Then:
1. Add it to the **Agents** table above and to each platform entry point (`.github/copilot-instructions.md`, `.cursorrules`, `CLAUDE.md`).
2. Create a `.github/agents/<name>.agent.md` wrapper with `user-invocable: false` so it's only accessible as a subagent.
3. Add the agent name to the `agents` list in `.github/agents/orchestrator.agent.md` so the orchestrator can invoke it.

## Adding a Skill

Create a folder `skills/<name>/` with a `README.md`:

```markdown
# Skill Name

**Type:** Skill

## Description
What this skill does and when to use it.

## When to Use
- Trigger conditions

## Procedure
1. Step-by-step instructions
```

Then add it to the **Skills** table above and to each platform entry point.
