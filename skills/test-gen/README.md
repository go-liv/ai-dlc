# Test Gen

**Type:** Skill  
**Agents:** Developer

## Description
Generates test cases from existing code and requirements. Analyzes functions, classes, and modules to produce comprehensive test suites covering happy paths, edge cases, error scenarios, and boundary conditions.

## When to Use
- After implementing a new feature that needs test coverage
- When adding tests to existing untested code
- When the Developer needs to verify edge cases
- When writing tests before implementation (TDD — generate test shells from requirements)
- When increasing test coverage for a module

## Procedure

### 1. Analyze the Target
Read the code to be tested and identify:
- **Public API surface**: Functions, methods, and classes to test
- **Input types and ranges**: What parameters does it accept?
- **Output types**: What does it return or produce?
- **Side effects**: Does it write to files, call APIs, modify state?
- **Dependencies**: What does it import or inject that needs mocking?
- **Error conditions**: What can go wrong and how is it handled?

### 2. Discover Test Conventions
Search the codebase for existing tests:
- **Test framework**: Jest, Mocha, pytest, xUnit, etc.
- **File naming**: `*.test.ts`, `*.spec.ts`, `test_*.py`, `*_test.go`, etc.
- **Directory structure**: Co-located with source or in a separate `test/` directory?
- **Patterns**: How are tests organized? (describe/it, Arrange-Act-Assert, Given-When-Then)
- **Mocking**: What mocking library is used? How are dependencies mocked?
- **Fixtures**: How is test data set up?

### 3. Design Test Cases
For each public function/method, create test cases across categories:

#### Happy Path
- Standard input produces expected output
- Common use cases work correctly

#### Edge Cases
- Empty inputs (null, undefined, empty string, empty array)
- Boundary values (0, -1, MAX_INT, empty collections)
- Single-element collections
- Very large inputs

#### Error Scenarios
- Invalid input types or formats
- Missing required parameters
- Dependency failures (network errors, DB timeouts)
- Permission/authorization failures

#### State Transitions (if applicable)
- Initial state is correct
- Transitions produce expected states
- Invalid transitions are rejected

### 4. Generate Test Code
Write the tests following project conventions:
- Match existing test file structure exactly
- Use the project's assertion style
- Mock dependencies the same way existing tests do
- Use descriptive test names that explain the scenario

### 5. Verify
- Run the tests to confirm they compile and execute
- Ensure passing tests actually test the right behavior (not trivially passing)
- Check that failing tests fail for the right reason

## Output Format

```markdown
## Tests Generated: <target module/function>

### File: `<test file path>`
<generated test code>

### Coverage Summary
| Function | Happy Path | Edge Cases | Errors | Total |
|----------|-----------|------------|--------|-------|
| <fn> | <count> | <count> | <count> | <count> |

### Notes
- <Any assumptions made>
- <Scenarios that need manual/integration testing>
```

## Constraints
- MATCH the project's existing test framework and conventions exactly
- DO NOT write trivial tests that don't verify meaningful behavior
- DO NOT test private/internal implementation details — test through the public API
- INCLUDE at least one edge case and one error case per function
- USE descriptive test names that explain the scenario being tested
- MOCK external dependencies — tests should be deterministic and fast
