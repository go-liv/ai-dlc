# Document

**Type:** Skill  
**Agents:** Architect, Designer, Developer, Product Owner

## Description
Generates or updates project documentation by reading the codebase and existing docs, then producing clear, accurate documentation targeted at the specified audience. Handles READMEs, API docs, onboarding guides, and technical references.

## When to Use
- When a project has no documentation or documentation is outdated
- After implementing features that need user-facing or developer docs
- When onboarding new team members requires written context
- To generate API documentation from code
- To update existing docs after architecture or design changes

## Procedure

### 1. Determine Documentation Type
Clarify what kind of documentation is needed:
- **README**: Project overview, setup, and usage
- **API Reference**: Endpoint/function documentation from code
- **Architecture Overview**: High-level system description for developers
- **Onboarding Guide**: Step-by-step getting-started for new contributors
- **Changelog**: Summary of changes for a release
- **Custom**: User-specified documentation format

### 2. Gather Source Material
Read all relevant inputs:
- Source code (public APIs, exports, main entry points)
- Existing documentation (to update, not duplicate)
- Architecture and design decision records
- Configuration files (package.json, docker-compose, CI configs)
- Test files (for usage examples)

### 3. Draft the Document
Write the documentation following these principles:
- **Audience-appropriate**: Technical depth matches the intended reader
- **Example-driven**: Include code examples, commands, or screenshots where helpful
- **Scannable**: Use headings, bullet points, and tables for quick navigation
- **Accurate**: Every claim must match the actual code — no aspirational docs
- **Minimal**: Don't document obvious things; focus on what's non-trivial

### 4. Place the Document
- Write to the path the user specifies
- Default locations: `README.md` (root), `docs/<topic>.md`, or inline in code
- If updating an existing file, preserve its structure and only modify relevant sections
- Ask before overwriting existing documentation

## Output Format
Depends on the documentation type. Always use Markdown. Structure should match the conventions already in the project, or use standard formats if none exist.

## Constraints
- DO NOT invent features or APIs that don't exist in the code
- DO NOT duplicate information already well-documented elsewhere — link to it instead
- DO NOT add generic filler content ("This project is great because...")
- KEEP documentation in sync with actual code — flag any discrepancies found
- PRESERVE existing documentation structure when updating
