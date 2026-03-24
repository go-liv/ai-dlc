# AI DLC

A library of reusable AI agents and skills. Works across VS Code Copilot, Cursor, and Claude.

## Setup

### VS Code Copilot (full native integration)

**Option A — GitHub URL (no clone, prompt-driven):**
1. In Copilot Chat, type `#` or run **Chat: Add Context**
2. Select **GitHub Repository**
3. Paste this repo's URL
4. Reference agents by name in your prompts (e.g., "act as the architect agent")

**Option B — Workspace folder (agent picker + auto-routing):**
1. Clone this repo
2. `File > Add Folder to Workspace...` → select the `ai-dlc` folder
3. Agents appear in the **agent picker** dropdown in chat — select one and type your prompt
4. Skills are auto-discovered — agents choose the right skill based on your prompt

> Option B is the most seamless experience: pick an agent from the dropdown, type a prompt, and skills are routed automatically.

### Cursor (prompt-driven)

Cursor doesn't have a native agent picker. The LLM follows agent/skill instructions when you reference them.

**Option A — Docs index (no clone):**
1. Go to **Cursor Settings > Features > Docs**
2. Add this repo's GitHub URL
3. In chat, type `@Docs` to pull in the repo as context
4. Reference agents by name (e.g., "act as the developer agent")

**Option B — Workspace folder:**
1. Clone this repo
2. Add it as a workspace folder
3. Cursor auto-reads `.cursorrules`, which indexes all agents and skills
4. Reference agents by name in your prompts

### Claude (prompt-driven)

Claude doesn't have a native agent picker. The LLM follows agent/skill instructions when you reference them.

**Claude Projects (web, no clone):**
1. Create or open a Project on claude.ai
2. In Project Knowledge, add this repo's GitHub URL or upload the files
3. Claude reads `CLAUDE.md` as the index
4. Reference agents by name (e.g., "act as the brainstormer agent")

**Claude Code (CLI):**
1. Clone this repo into or alongside your project
2. Claude Code auto-reads `CLAUDE.md`
3. Reference agents by name in your prompts

### Platform Comparison

| Feature | VS Code Copilot (workspace) | VS Code Copilot (URL) | Cursor | Claude |
|---------|---------------------------|----------------------|--------|--------|
| Agent picker UI | Yes | No | No | No |
| Skill auto-routing | Yes | No | No | No |
| Prompt-driven agents | Yes | Yes | Yes | Yes |
| Clone required | Yes | No | No | No* |

\* Claude Projects can index a GitHub URL directly; Claude Code requires a clone.

## Usage Examples

### VS Code Copilot (workspace folder — native)

Agents appear in the picker dropdown. Skills are auto-routed.

**Selecting an agent:**
1. Open Copilot Chat
2. Click the agent picker (dropdown at the top of chat)
3. Select **architect**, **developer**, etc.
4. Type your prompt — the agent persona is active automatically

**Agent + auto-routed skill:**
> *[Select `developer` from picker]*
> "Set up a new Express API with health check endpoint"
>
> The developer agent activates and picks the relevant skill if one matches.

**Using an agent via prompt (URL setup):**
> "Act as the architect agent from ai-dlc. I need to decide between a monolith and microservices for a new e-commerce platform."

**Invoking a skill directly (slash command):**
> Type `/hello-world` in chat to invoke the skill by name.

---

### Cursor

Reference agents and skills by name in your prompt. If using `@Docs`, Cursor pulls in the repo context.

**Using an agent:**
> "@Docs act as the architect agent. I'm building a real-time notification system and need to choose between WebSockets, SSE, and polling."

**Using an agent (workspace folder):**
> "Act as the developer agent. Refactor the auth middleware in `src/middleware/auth.ts` to use JWT verification."

**Using a skill:**
> "Follow the hello-world skill from ai-dlc to verify the setup is working."

**Combining agent + skill:**
> "Act as the developer agent. Use the hello-world skill to scaffold something and verify my DLC setup."

---

### Claude

Reference agents and skills by name. Claude reads the index and follows the linked instructions.

**Using an agent (Claude Projects):**
> "Act as the brainstormer agent. I want to build a CLI tool for managing dotfiles but I'm not sure what language or approach to use."

**Using an agent (Claude Code):**
> "Act as the explorer agent. Find all the places where we handle authentication errors and summarize the patterns used."

**Using a skill:**
> "Follow the hello-world skill procedure to verify this DLC repo is accessible."

**Combining agent + context:**
> "Act as the architect agent. Look at the files in `src/services/` and propose options for breaking the payment service into its own module."

## How It Works

```
ai-dlc/
├── agents/                          # Canonical agent definitions (any LLM)
│   ├── architect.md
│   ├── brainstormer.md
│   ├── developer.md
│   └── explorer.md
├── skills/                          # Canonical skill definitions (any LLM)
│   └── hello-world/
│       └── README.md
├── .github/
│   ├── copilot-instructions.md      # Copilot: workspace instructions (index)
│   ├── agents/                      # Copilot: native agent picker entries
│   │   ├── architect.agent.md
│   │   ├── brainstormer.agent.md
│   │   ├── developer.agent.md
│   │   └── explorer.agent.md
│   └── skills/                      # Copilot: native skill auto-routing
│       └── hello-world/
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
| [architect](agents/architect.md) | Proposes architecture options with trade-offs, records decisions as ADRs |
| [brainstormer](agents/brainstormer.md) | Collaborative ideation partner, backs up answers with evidence |
| [developer](agents/developer.md) | Implements features, fixes, and refactors based on user context |
| [explorer](agents/explorer.md) | Read-only codebase exploration and Q&A |

## Skills

| Skill | Description |
|-------|-------------|
| [hello-world](skills/hello-world/README.md) | Example template for creating new skills |

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

Then add it to the **Agents** table above and to each platform entry point (`.github/copilot-instructions.md`, `.cursorrules`, `CLAUDE.md`).

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
