# Plan

**Type:** Skill

## Description
Generates a detailed work plan by reading all available project context — business requirements, architecture decisions, design documents, and any other related files — then producing a structured plan that downstream agents (Developer, Architect, etc.) can follow to build the product.

## When to Use
- At the start of a project or feature to create an actionable development plan
- When business context, requirements, or architecture documents exist and need to be translated into concrete work items
- Before handing off to Developer or other implementation agents
- To re-plan after scope changes or new discoveries

## Procedure

### 1. Discover Context
Scan the workspace for all files that may contain relevant product context. Look for:
- Business requirements and PRDs (`**/requirements/**`, `**/docs/**`, `**/prd*`, `**/*requirements*`, `**/*spec*`)
- Architecture Decision Records (`**/adr/**`, `**/decisions/**`, `**/*adr*`)
- Design documents (`**/*design*`, `**/*architecture*`, `**/*proposal*`)
- Existing plans or roadmaps (`**/*plan*`, `**/*roadmap*`, `**/*backlog*`)
- README files at every level (`**/README.md`)
- User stories or epics (`**/*stories*`, `**/*epics*`, `**/*user-stor*`)
- API specs or contracts (`**/*openapi*`, `**/*swagger*`, `**/*api*`)
- Existing source code structure (top-level directories)

### 2. Read and Synthesize
Read every discovered file. Extract:
- **Goals**: What the product or feature must achieve
- **Constraints**: Technical, business, or timeline constraints
- **Decisions already made**: Architecture choices, tech stack, patterns
- **Open questions**: Ambiguities or gaps in the documentation
- **Dependencies**: External services, libraries, or teams

### 3. Generate the Plan
Produce a structured plan in Markdown with the following sections:

```markdown
# Work Plan — <Product/Feature Name>

## Summary
One-paragraph overview of what will be built and why.

## Goals
Bulleted list of measurable objectives extracted from the context.

## Constraints
Technical, business, and timeline constraints that shape the work.

## Assumptions
Anything assumed but not explicitly stated in the source documents.

## Open Questions
Unresolved items that need answers before or during implementation.

## Work Phases
Ordered phases, each containing:
### Phase N: <Phase Name>
**Objective:** What this phase achieves.
**Depends on:** Previous phases or external dependencies.
#### Tasks
- [ ] Task description — brief rationale
- [ ] ...
#### Deliverables
- What is produced at the end of this phase.

## Dependencies
External services, APIs, libraries, or teams required.

## Risks
Known risks and suggested mitigations.
```

### 4. Output
- Write the plan to `docs/plan.md` (or the path the user specifies).
- If a plan already exists at the target path, present the updated plan and ask the user before overwriting.
- Summarize the plan to the user with the number of phases, total tasks, and any open questions that need resolution.

## Constraints
- **Read-only analysis**: Do not modify any source files; only read context and produce the plan document.
- **Evidence-based**: Every goal, constraint, and task must trace back to a discovered source file. Cite the source file when possible.
- **No hallucinated requirements**: If the context is insufficient, surface it as an open question rather than inventing details.
- **Agent-consumable output**: The plan must be clear enough that a Developer agent can pick up any phase and start implementing without additional clarification.
