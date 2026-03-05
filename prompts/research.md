# Research Phase

## Core Principle
Never write code until you've deeply understood the codebase. Cursory reading is insufficient.

## Instructions

### 1. Deep Exploration
Thoroughly examine the relevant codebase sections. Use deliberate language:
- "Deeply analyze the intricacies of..."
- "Examine in great detail how..."
- "Understand thoroughly the relationships between..."

Do NOT skim. Read every relevant file completely.

### 2. Find Reference Implementations
Search for similar patterns in the codebase:
- How have similar features been implemented before?
- What conventions does this codebase follow?
- Are there existing abstractions to leverage?

Document these as reference implementations to guide the plan.

### 3. Map Dependencies
- Identify all files, classes, and methods involved
- Trace the call graph in both directions
- Note external integrations and APIs
- Document database/schema dependencies

### 4. Capture Constraints
- API contracts that must be preserved
- Performance requirements
- Security considerations
- Backward compatibility needs

### 5. List Open Questions
- Ambiguities needing clarification
- Design decisions requiring input
- Trade-offs to discuss with me

## Output

Write findings to `~/boris/workstreams/{TICKET}/research.md`:

```markdown
# Research: {TICKET}

## Overview
What this task is about and why it matters

## Files Analyzed
| File | Purpose | Relevance |
|------|---------|-----------|
| path/to/file.java | Description | Why it matters |

## Reference Implementations
Similar patterns found in the codebase that we can follow

## Key Findings
- Finding 1
- Finding 2

## Dependencies
- Upstream: what calls this
- Downstream: what this calls

## Constraints
- Must preserve X
- Cannot break Y

## Open Questions
- Question 1
- Question 2
```

## IMPORTANT
- DO NOT write any code
- DO NOT propose solutions yet
- Focus ONLY on understanding
- This artifact is my review surface to catch misunderstandings early
