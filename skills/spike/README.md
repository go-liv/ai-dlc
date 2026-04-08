# Spike

**Type:** Skill  
**Agents:** Brainstormer, Architect

## Description
Conducts a time-boxed technical investigation (spike) to reduce uncertainty around a specific technical question. Produces a findings report with concrete answers, proof-of-concept code (if applicable), and a go/no-go recommendation.

## When to Use
- When a technical approach is uncertain and needs validation before committing
- When evaluating whether a library, API, or pattern works for the use case
- Before the Architect commits to a design that depends on unverified assumptions
- When the Brainstormer identifies a technical unknown that blocks decision-making

## Procedure

### 1. Define the Spike
Clearly scope the investigation:
- **Question**: What specific technical question needs answering?
- **Success criteria**: What would a successful outcome look like?
- **Scope boundary**: What is explicitly out of scope?

### 2. Plan the Investigation
Outline the steps to answer the question:
1. What to research (docs, source code, examples)
2. What to prototype (if a proof of concept is needed)
3. What to test (performance benchmarks, compatibility checks)

### 3. Execute
Perform the investigation:
- Read documentation and source code
- Search for existing examples, issues, or known limitations
- Build a minimal proof of concept if needed (keep it throwaway — not production code)
- Run benchmarks or compatibility tests if applicable

### 4. Assess Findings
Evaluate results against the success criteria:
- **Feasible**: Works as expected, ready to proceed
- **Feasible with caveats**: Works but with limitations or trade-offs
- **Not feasible**: Doesn't work or has deal-breaking limitations

### 5. Report

## Output Format

```markdown
# Spike Report — <Question>

## Question
<The specific technical question being investigated>

## Success Criteria
- <criterion 1>
- <criterion 2>

## Findings

### What Was Tried
1. <approach 1> — <result>
2. <approach 2> — <result>

### Key Discoveries
- <discovery 1 with evidence>
- <discovery 2 with evidence>

### Proof of Concept (if applicable)
<Code snippet or link to throwaway prototype>
<How to run it and what it demonstrates>

### Limitations Found
- <limitation 1>
- <limitation 2>

## Verdict: <Feasible | Feasible with Caveats | Not Feasible>
<Clear rationale>

## Recommendation
<What to do next based on findings>

## Sources
- [Source 1](url) — <description>
```

## Constraints
- KEEP the scope tight — answer the specific question, don't expand into adjacent topics
- PROOF OF CONCEPT code is throwaway — mark it clearly as such, do not merge into the project
- REPORT both positive and negative findings — don't cherry-pick results
- TIME-BOX the effort — if the investigation isn't converging, report what was found and what remains unknown
- ALWAYS end with a clear verdict and recommendation
