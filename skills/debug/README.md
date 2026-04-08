# Debug

**Type:** Skill  
**Agents:** Developer

## Description
Systematic debugging workflow that methodically narrows down the root cause of a bug through hypothesis-driven investigation. Produces a diagnosis report with the root cause, affected code paths, and a recommended fix.

## When to Use
- When a bug is reported and the cause isn't obvious
- When error messages or stack traces need to be traced to root cause
- When a test is failing and the reason is unclear
- When behavior diverges from expectations and the Developer needs a structured approach

## Procedure

### 1. Define the Bug
Capture the problem clearly:
- **Observed behavior**: What actually happens?
- **Expected behavior**: What should happen?
- **Reproduction steps**: How to trigger the bug (if known)
- **Error output**: Stack traces, logs, error messages

### 2. Form Hypotheses
Based on the symptoms, generate 2-4 likely causes:
- Rank by probability (most likely first)
- For each hypothesis, identify what evidence would confirm or rule it out

```markdown
| # | Hypothesis | Evidence Needed | Probability |
|---|-----------|----------------|-------------|
| 1 | <cause> | <what to check> | High |
| 2 | <cause> | <what to check> | Medium |
| 3 | <cause> | <what to check> | Low |
```

### 3. Investigate Systematically
For each hypothesis (starting with highest probability):
1. Search for the relevant code paths
2. Read the code to understand the actual flow
3. Check for the specific condition that would cause the bug
4. Look at recent changes to the affected code
5. Check test coverage for the failure case

Mark each hypothesis as **Confirmed**, **Ruled Out**, or **Inconclusive**.

### 4. Identify Root Cause
Once a hypothesis is confirmed:
- Trace the full chain: trigger → root cause → symptom
- Identify all code paths affected by the same root cause
- Check if there are related bugs caused by the same issue

### 5. Recommend Fix
Propose the minimal fix:
- What code needs to change and why
- What tests should be added to prevent regression
- Whether the fix has any side effects

## Output Format

```markdown
# Debug Report — <Bug Title>

## Symptoms
- **Observed**: <what happens>
- **Expected**: <what should happen>
- **Error**: <error message or stack trace>

## Investigation

### Hypothesis 1: <description> — **Confirmed** ✓
<Evidence found, code paths traced>

### Hypothesis 2: <description> — **Ruled Out** ✗
<Why this wasn't the cause>

## Root Cause
<Clear explanation of exactly what causes the bug>

**File**: <file path>  
**Line**: <line number(s)>  
**Trigger**: <what conditions cause the bug to manifest>

## Affected Code Paths
- <path 1>: <how it's affected>
- <path 2>: <how it's affected>

## Recommended Fix
<Description of the fix>

### Code Change
<The specific code change or diff>

### Tests to Add
- <Test case 1: what to assert>
- <Test case 2: edge case>

## Prevention
<What could prevent similar bugs: better validation, type safety, tests, etc.>
```

## Constraints
- DO NOT jump to a fix without confirming the root cause
- DO NOT modify code during investigation — diagnose first, fix second
- TEST each hypothesis against evidence — don't assume
- KEEP the investigation log even for ruled-out hypotheses — they provide useful context
- ALWAYS recommend tests that would catch this bug in the future
