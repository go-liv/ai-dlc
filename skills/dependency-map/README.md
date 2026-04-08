# Dependency Map

**Type:** Skill  
**Agents:** Explorer

## Description
Traces and maps code dependencies within a project — module imports, function call chains, service interactions, and data flows. Produces a structured dependency report that helps understand how components connect.

## When to Use
- When understanding how a module or function fits into the larger system
- Before refactoring to identify all affected code paths
- When tracing a bug through layers of the application
- When onboarding to understand project structure
- When the Architect needs dependency info to evaluate a design change

## Procedure

### 1. Define the Starting Point
Determine what to trace:
- **Module/file**: All imports into and exports from a specific file
- **Function/class**: All callers and callees of a specific symbol
- **Service**: All interactions between services (HTTP calls, message queues, etc.)
- **Data entity**: How a data model flows through the system

### 2. Trace Outgoing Dependencies
From the starting point, find everything it depends on:
- Direct imports and requires
- Function/method calls to other modules
- External service calls (HTTP, DB, message queues)
- Configuration dependencies

### 3. Trace Incoming Dependencies
Find everything that depends on the starting point:
- Files that import this module
- Functions that call this function
- Services that call this endpoint
- Tests that exercise this code

### 4. Identify Dependency Patterns
Flag notable patterns:
- **Circular dependencies**: A → B → C → A
- **Hub modules**: Files imported by many others (high fan-in)
- **Deeply coupled chains**: Long dependency chains that increase fragility
- **External boundaries**: Where internal code meets external APIs/libraries

### 5. Generate the Map

## Output Format

```markdown
# Dependency Map — <Starting Point>

## Overview
<What was traced and why>

## Direct Dependencies (outgoing)
| Dependency | Type | File/Service |
|-----------|------|-------------|
| <name> | import | <path> |
| <name> | API call | <endpoint> |
| <name> | DB query | <table/collection> |

## Dependents (incoming)
| Dependent | Type | File/Service |
|-----------|------|-------------|
| <name> | import | <path> |
| <name> | function call | <path:function> |

## Dependency Chain
```
<starting point>
├── dependency-1
│   ├── sub-dep-1a
│   └── sub-dep-1b
├── dependency-2
└── dependency-3
    └── sub-dep-3a
```

## Patterns Detected
- **Circular**: <description if found>
- **High fan-in**: <modules imported by many files>
- **High fan-out**: <modules that import many others>

## Impact Analysis
If `<starting point>` changes:
- **Directly affected**: <list of files/modules>
- **Transitively affected**: <list of files that depend on the above>
- **Test coverage**: <which test files exercise this code>

## Recommendations
- <Suggestions for reducing coupling if applicable>
```

## Constraints
- DO NOT modify any files — this is a read-only analysis
- TRACE at least 2 levels deep for outgoing dependencies
- VERIFY dependencies by reading actual import statements — do not guess
- FLAG circular dependencies prominently
- INCLUDE test files in the incoming dependency analysis
