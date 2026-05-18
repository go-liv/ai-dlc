# SonarQube Fix

**Type:** Skill  
**Agents:** QA Engineer, Developer

## Description
Connects to SonarQube Web API to retrieve code quality findings (bugs, vulnerabilities, code smells, security hotspots), analyzes them in context, and implements fixes. Supports filtering by severity, type, and scope.

## When to Use
- When SonarQube reports quality issues that need remediation
- When preparing code for a quality gate
- When systematically reducing technical debt
- When addressing security vulnerabilities identified by SonarQube
- When fixing code smells or maintainability issues

## Procedure

### 1. Connect to SonarQube

#### Configuration

Connection details are stored in `skills/sonarqube-fix/.env` within the ai-dlc repo. This keeps the configuration portable — set it up once and it works regardless of which project you're analyzing.

##### Setup

1. Copy the example file:
   ```
   cp skills/sonarqube-fix/.env.example skills/sonarqube-fix/.env
   ```
2. Fill in your values in `skills/sonarqube-fix/.env`

##### `skills/sonarqube-fix/.env.example` (committed to repo)

```env
# SonarQube connection — copy this file to .env and fill in values
SONAR_HOST_URL=https://sonarqube.example.com
SONAR_PROJECT_KEY=my-project-key
SONAR_TOKEN=
SONAR_BRANCH=main
```

##### `skills/sonarqube-fix/.env` (gitignored)

```env
SONAR_HOST_URL=https://sonarqube.example.com
SONAR_PROJECT_KEY=my-project-key
SONAR_TOKEN=squ_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
SONAR_BRANCH=main
```

> **Note**: The `.env` file is gitignored. The `.env.example` serves as the template for anyone cloning the repo.

#### Resolution Order

| Setting | 1st: `skills/sonarqube-fix/.env` | 2nd: Shell env var | 3rd: Ask user |
|---------|----------------------------------|--------------------:|---------------|
| Server URL | `SONAR_HOST_URL` | `SONAR_HOST_URL` | Prompt |
| Project Key | `SONAR_PROJECT_KEY` | `SONAR_PROJECT_KEY` | Prompt |
| Token | `SONAR_TOKEN` | `SONAR_TOKEN` | Prompt (do not persist) |
| Branch | `SONAR_BRANCH` | `SONAR_BRANCH` | Current branch or `main` |

> Read `skills/sonarqube-fix/.env` first. If a value is missing, check shell environment variables. Only ask the user as a last resort.

#### API Usage

Once connection details are resolved, use the SonarQube Web API:
- `GET /api/issues/search?componentKeys={projectKey}&statuses=OPEN,CONFIRMED,REOPENED&ps=100`
- Filter by severity: `&severities=BLOCKER,CRITICAL,MAJOR,MINOR,INFO`
- Filter by type: `&types=BUG,VULNERABILITY,CODE_SMELL,SECURITY_HOTSPOT`
- Filter by file: `&files={filePath}` (when scoping to specific files)
- Pagination: `&p={page}` for subsequent pages

### 2. Retrieve and Categorize Issues
Parse the API response and categorize findings:

| Category | Priority | Action |
|----------|----------|--------|
| BLOCKER/CRITICAL Bugs | P1 | Fix immediately |
| Vulnerabilities | P2 | Fix with security context |
| MAJOR Code Smells | P3 | Fix if in scope |
| MINOR/INFO | P4 | Fix opportunistically |

For each issue, extract:
- Rule key and description (`/api/rules/show?key={ruleKey}`)
- Affected file and line range
- Issue message and effort estimate
- Flow locations (for data-flow issues)

### 3. Analyze in Context
For each issue (starting with highest priority):
- Read the affected file and surrounding code
- Understand the rule being violated (what it checks and why)
- Determine if it's a true positive or false positive
- If false positive: document why and mark with `// NOSONAR` or appropriate suppression (only if genuinely not applicable)
- If true positive: plan the fix

### 4. Implement Fixes
For each true positive:
- Apply the minimal fix that resolves the finding
- Ensure the fix doesn't introduce new issues
- Follow existing code conventions
- Group related fixes (e.g., same rule across multiple locations)

Common fix patterns:
- **Null checks**: Add appropriate null handling
- **Resource leaks**: Add proper disposal/close
- **SQL injection**: Use parameterized queries
- **XSS**: Add output encoding
- **Complexity**: Extract methods, simplify conditions
- **Duplications**: Extract shared logic
- **Dead code**: Remove unused code
- **Naming conventions**: Rename to follow standards

### 5. Verify
- Confirm the fix addresses the specific rule violation
- Run existing tests to ensure no regressions
- Check that the fix doesn't trigger other SonarQube rules

### 6. Report
Produce a summary of actions taken.

## Output Format

```markdown
## SonarQube Remediation Report

### Connection
- **Server**: {url}
- **Project**: {projectKey}
- **Branch**: {branch}

### Summary
| Severity | Found | Fixed | Suppressed | Remaining |
|----------|-------|-------|------------|-----------|
| BLOCKER | X | X | 0 | 0 |
| CRITICAL | X | X | 0 | 0 |
| MAJOR | X | X | X | X |
| MINOR | X | X | X | X |

### Fixes Applied
#### {Rule Key}: {Rule Name}
- **File**: {path}:{line}
- **Issue**: {description}
- **Fix**: {what was changed and why}

### Suppressed (False Positives)
#### {Rule Key}: {Rule Name}
- **File**: {path}:{line}
- **Reason**: {why this is not applicable}

### Remaining Issues
- {Issues not addressed and why (e.g., requires architectural change, out of scope)}
```

## Constraints
- NEVER store or log authentication tokens
- DO NOT suppress issues without clear justification
- PRIORITIZE by severity — fix blockers and criticals first
- DO NOT make unrelated code changes while fixing issues
- VERIFY fixes don't break existing tests
- RESPECT the project's existing patterns and conventions
