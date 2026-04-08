# ADR

**Type:** Skill  
**Agents:** Architect

## Description
Manages the full lifecycle of Architecture Decision Records — creating, listing, updating, and superseding ADRs. Provides a consistent format and numbering scheme, and maintains an ADR index.

## When to Use
- When the Architect proposes options and the user picks one — record the decision
- When revisiting a past decision that needs to be updated or superseded
- When listing or searching existing architecture decisions
- When onboarding someone who needs to understand why decisions were made

## Procedure

### 1. Determine the Action
- **Create**: Record a new architecture decision
- **List**: Show all existing ADRs with their status
- **Update**: Modify the status or content of an existing ADR
- **Supersede**: Mark an ADR as superseded and link to its replacement

### 2. Discover Existing ADRs
Search for the architecture file or ADR directory:
- Check for `docs/architecture.md` (single-file format)
- Check for `docs/adr/` directory (multi-file format)
- Check for any `**/adr*` or `**/decisions*` files
- If nothing exists, use single-file format at `docs/architecture.md`

### 3. Assign Number
- Read existing ADRs to find the highest number
- Assign the next sequential number (ADR-001, ADR-002, etc.)
- Never reuse numbers from superseded ADRs

### 4. Write the Record

#### Single-File Format (append to `docs/architecture.md`)
```markdown
## ADR-<NNN>: <Title>

**Date:** <YYYY-MM-DD>  
**Status:** Accepted | Superseded by ADR-<NNN> | Deprecated  

### Context
<The problem, forces, and constraints that led to this decision>

### Options Considered
1. **<Option>** — <one-line summary>
2. **<Option>** — <one-line summary>

### Decision
<Chosen option and clear rationale>

### Consequences
- <Positive consequences>
- <Negative consequences or trade-offs accepted>
- <Follow-up actions required>
```

#### Multi-File Format (create `docs/adr/NNN-title.md`)
Same structure as above, but as a standalone file with a `# ADR-<NNN>: <Title>` H1 heading.

### 5. Update Index
If using multi-file format, update `docs/adr/README.md`:
```markdown
| ADR | Title | Status | Date |
|-----|-------|--------|------|
| [ADR-001](001-title.md) | Title | Accepted | 2024-01-15 |
```

## Constraints
- NEVER create an ADR without a clear decision — if the decision hasn't been made yet, use the Architect's proposal workflow instead
- ALWAYS include options considered — even if only one option was viable, document why alternatives were rejected
- PRESERVE existing ADRs — never delete or modify the decision of an accepted ADR; supersede it instead
- USE consistent numbering — never skip or reuse numbers
