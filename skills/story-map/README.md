# Story Map

**Type:** Skill  
**Agents:** Product Owner

## Description
Creates a user story map that organizes features into user activities, user tasks, and user stories — arranged by priority. Produces a structured document that serves as a living backlog with clear release boundaries.

## When to Use
- When starting a new product or major feature
- When the Product Owner needs to organize a large backlog
- When planning releases and defining MVP scope
- After gathering requirements to structure them into deliverables
- When re-prioritizing work after scope changes

## Procedure

### 1. Identify User Personas
From project context, extract or define the key user types:
- Who are the primary users?
- What are their goals and pain points?
- What distinguishes each persona?

### 2. Map User Activities
Identify the high-level activities users perform (the "backbone"):
- These are broad categories of work the user does
- Arrange them left-to-right in the order users typically encounter them
- Example: Sign Up → Configure → Create Content → Share → Analyze

### 3. Break Down into Tasks
Under each activity, list the specific tasks (the "walking skeleton"):
- These are the concrete steps within each activity
- Keep them at a level that represents meaningful user actions

### 4. Write User Stories
Under each task, write detailed user stories:
- Follow the format: "As a [persona], I want [action] so that [benefit]"
- Apply INVEST criteria (Independent, Negotiable, Valuable, Estimable, Small, Testable)
- Include acceptance criteria for each story

### 5. Define Release Slices
Draw horizontal lines to define release boundaries:
- **Release 1 (MVP)**: Minimum stories needed for a usable product
- **Release 2**: Stories that improve core experience
- **Release 3+**: Nice-to-haves and extensions

### 6. Produce the Map

## Output Format

```markdown
# Story Map — <Product/Feature Name>

## Personas
### <Persona 1>
- **Role**: <who they are>
- **Goal**: <what they want to achieve>
- **Pain points**: <current frustrations>

## Story Map

### Activity: <Activity 1>

#### Task: <Task 1.1>

**Release 1 (MVP)**
- [ ] **US-001**: As a <persona>, I want <action> so that <benefit>
  - AC: <acceptance criteria>
  - AC: <acceptance criteria>

- [ ] **US-002**: As a <persona>, I want <action> so that <benefit>
  - AC: <acceptance criteria>

**Release 2**
- [ ] **US-003**: As a <persona>, I want <action> so that <benefit>
  - AC: <acceptance criteria>

#### Task: <Task 1.2>
...

### Activity: <Activity 2>
...

## Dependencies
- US-003 depends on US-001
- ...

## Metrics
| Metric | Target | Measured By |
|--------|--------|-------------|
| <metric> | <target> | <how> |

## Open Questions
- <question needing clarification>
```

Write the story map to `docs/story-map.md` (or user-specified path).

## Constraints
- EVERY story must follow the "As a... I want... So that..." format
- EVERY story must have at least one acceptance criterion
- STORIES must be independent enough to implement and test in isolation
- RELEASE 1 must be a viable MVP — not just a partial feature
- DO NOT create stories for implementation details — stories describe user value
- NUMBER stories sequentially (US-001, US-002, ...) for easy reference
