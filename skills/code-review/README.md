# Code Review

**Type:** Skill  
**Agents:** Developer, Architect, Explorer

## Description
Performs a systematic code review on a given file, directory, or changeset. Checks for correctness, style consistency, security vulnerabilities, performance issues, and adherence to project conventions.

## When to Use
- Before merging or finalizing a feature implementation
- When the user asks to review code quality or find issues
- As part of a Developer workflow after implementing changes
- When the Architect wants to verify implementation matches the decided architecture
- When the Explorer is asked to assess code quality

## Procedure

### 1. Identify Scope
Determine what to review:
- **Specific files**: The user provides file paths
- **Changed files**: Diff-based review of recent modifications
- **Directory**: Review all source files in a directory

### 2. Gather Context
Before reviewing, understand the project:
- Read project conventions (linter config, `.editorconfig`, style guides)
- Identify the language/framework and its idioms
- Check for existing tests related to the code under review

### 3. Review Checklist
Evaluate the code against each category:

#### Correctness
- Does the code do what it's supposed to?
- Are edge cases handled?
- Are error paths handled appropriately?

#### Security (OWASP Top 10)
- Input validation and sanitization
- Authentication and authorization checks
- No hardcoded secrets or credentials
- Proper use of parameterized queries (no SQL injection)
- No unsafe deserialization or injection vectors

#### Style & Conventions
- Follows existing naming conventions in the project
- Consistent formatting and indentation
- No dead code or commented-out blocks
- Imports are organized per project convention

#### Performance
- No obvious N+1 queries or unnecessary loops
- Appropriate data structures for the use case
- No unnecessary allocations in hot paths

#### Maintainability
- Functions and classes have a single responsibility
- No excessive nesting or complexity
- Meaningful variable and function names
- Dependencies are explicit, not hidden

#### Tests
- Are there tests for the new/changed code?
- Do existing tests still pass?
- Are edge cases covered?

### 4. Generate Report
Produce a structured review with findings categorized by severity.

## Output Format

```markdown
# Code Review — <scope description>

## Summary
<One-paragraph overall assessment>

## Findings

### Critical
- **[file:line]** <description> — <suggested fix>

### Warning
- **[file:line]** <description> — <suggested fix>

### Suggestion
- **[file:line]** <description> — <suggested improvement>

## Verdict
<APPROVE | REQUEST_CHANGES | NEEDS_DISCUSSION>
<Brief rationale>
```

## Constraints
- DO NOT auto-fix issues unless the user explicitly asks for it
- DO NOT flag stylistic preferences that contradict existing project conventions
- PRIORITIZE findings by severity — critical issues first
- CITE specific file paths and line numbers for every finding
- KEEP suggestions actionable — always include a suggested fix or improvement
