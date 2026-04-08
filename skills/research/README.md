# Research

**Type:** Skill  
**Agents:** Brainstormer, Architect, Designer

## Description
Conducts structured research on technologies, patterns, libraries, or approaches. Gathers evidence from documentation, articles, and existing codebases to inform decisions. Produces a research brief that other agents can act on.

## When to Use
- When evaluating a new technology, library, or framework
- Before making architecture or design decisions
- When the Brainstormer needs evidence to support or challenge ideas
- When comparing multiple approaches to a problem
- When building context on an unfamiliar domain

## Procedure

### 1. Define the Research Question
State the question(s) to answer clearly:
- What are we trying to learn?
- What decision will this research inform?
- What are the evaluation criteria?

### 2. Search for Evidence
Use available tools to gather information:
- **Codebase**: Search for existing usage patterns, prior art, or related implementations
- **Documentation**: Fetch official docs for relevant technologies
- **Web**: Search for comparisons, benchmarks, case studies, and community feedback
- **Project history**: Check for previous decisions or discussions on the topic

### 3. Evaluate Sources
For each piece of evidence:
- Note the source and its credibility
- Extract the relevant facts or data points
- Flag any biases or limitations (e.g., vendor marketing vs. independent benchmarks)

### 4. Synthesize Findings
Organize the evidence into a structured brief:
- Group by theme or evaluation criterion
- Note areas of consensus and disagreement
- Identify gaps where evidence is insufficient

### 5. Produce the Brief

## Output Format

```markdown
# Research Brief — <Topic>

## Question
<The research question or decision being informed>

## Key Findings
1. **<Finding>**: <Evidence summary> — *Source: [name](url)*
2. **<Finding>**: <Evidence summary> — *Source: [name](url)*
...

## Comparison Matrix (if applicable)
| Criterion | Option A | Option B | Option C |
|-----------|----------|----------|----------|
| <criterion> | <rating/notes> | <rating/notes> | <rating/notes> |

## Gaps & Unknowns
- <What couldn't be determined and why>

## Recommendation
<Suggested direction based on evidence, with confidence level: high/medium/low>

## Sources
- [Source 1](url) — <brief description>
- [Source 2](url) — <brief description>
```

## Constraints
- DO NOT present opinions as facts — always cite sources
- DO NOT rely on a single source — corroborate important claims
- DO NOT fabricate URLs or references — only cite sources you actually found
- CLEARLY distinguish between facts, interpretations, and your own judgment
- FLAG low-confidence findings explicitly
