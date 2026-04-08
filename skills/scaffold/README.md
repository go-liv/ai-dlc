# Scaffold

**Type:** Skill  
**Agents:** Developer

## Description
Generates boilerplate code by discovering existing patterns and conventions in the project, then replicating them for new components, modules, endpoints, or features. Ensures consistency with the codebase without manual template maintenance.

## When to Use
- When creating a new component, service, or module that should follow existing patterns
- When adding a new API endpoint to an existing set
- When creating a new test file that should match the project's test structure
- When the Developer needs to quickly set up the skeleton of a new feature

## Procedure

### 1. Identify What to Scaffold
Determine the type of code to generate:
- **Component**: UI component (React, Vue, Angular, etc.)
- **Service/Module**: Business logic module or service class
- **API Endpoint**: Route handler, controller, or resolver
- **Test**: Test file for existing code
- **Model**: Data model, schema, or entity
- **Config**: Configuration file following project patterns
- **Full feature**: Combination of the above

### 2. Discover Existing Patterns
Search the codebase for similar existing code:
- Find 2-3 existing examples of the same type
- Identify the common structure: file naming, directory placement, imports, exports
- Note project conventions: naming style, error handling patterns, logging approach
- Check for code generators or templates already in the project

### 3. Extract the Pattern
From the examples, extract:
- **File path convention**: Where does this type of file live?
- **Naming convention**: How are files, classes, functions named?
- **Boilerplate structure**: What's the skeleton every file of this type shares?
- **Dependencies**: What imports are always present?
- **Registration**: Does the new code need to be registered somewhere (routes file, module index, DI container)?

### 4. Generate the Code
Create files following the extracted pattern:
- Match the naming convention exactly
- Include all standard imports and boilerplate
- Add TODO comments where custom logic needs to be filled in
- Register the new code in any required index or config files

### 5. Verify
- Check that the generated code compiles/passes linting
- Verify the file is in the correct directory
- Confirm any registrations are complete

## Output Format
- Generated files with clear TODO markers for customization points
- Brief summary of what was created and what needs manual implementation

```markdown
## Scaffolded: <what was created>

### Files Created
- `<path>` — <purpose>
- `<path>` — <purpose>

### Registrations
- Added to `<path>` — <what was registered>

### TODO
- [ ] Implement <specific logic> in `<path>`
- [ ] Add tests for <specific behavior>
```

## Constraints
- ALWAYS discover patterns from the existing codebase — never apply generic templates
- MATCH file naming, directory structure, and coding style exactly
- MARK customization points with `// TODO:` comments — don't generate fake logic
- REGISTER new code in index files, route files, or DI containers as the project convention requires
- DO NOT generate code that duplicates something that already exists
