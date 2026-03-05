# Planning Phase

## Core Principle
Create a detailed, reviewable plan. This will go through multiple annotation cycles before implementation.

## Instructions

### 1. Review Context
- Read `~/boris/workstreams/{TICKET}/research.md`
- Read `~/boris/workstreams/{TICKET}/annotations.md` for my feedback
- Incorporate any corrections from previous iterations

### 2. Use Reference Implementations
- Base your approach on patterns found during research
- Propose solutions that match existing codebase conventions
- Note where you're deviating and why

### 3. Create Detailed Plan
For each file to modify:
- Exact file path
- Specific line numbers
- Code snippets for complex changes
- Order of changes (dependencies matter)

### 4. Identify Risks
- Edge cases to handle
- Potential breaking changes
- Performance implications
- Security considerations

### 5. Create Granular Todo List
- Actionable, specific items
- Ordered by dependency
- Include testing tasks
- Include documentation updates

## Output

Write to `~/boris/workstreams/{TICKET}/plan.md`:

```markdown
# Implementation Plan: {TICKET}

## Approach
Brief description based on reference implementations found

## Changes

### 1. File: path/to/file.java (lines X-Y)
**What:** Description
**Why:** Reasoning
**Code:**
\`\`\`java
// snippet
\`\`\`

### 2. File: path/to/another.java (lines A-B)
...

## Risks & Mitigations
| Risk | Impact | Mitigation |
|------|--------|------------|
| Risk 1 | High/Med/Low | How to handle |

## Todo
- [ ] Change 1 in file X
- [ ] Change 2 in file Y
- [ ] Write unit tests
- [ ] Update README if needed
- [ ] Manual testing steps
```

## Annotation Cycle

After I review, I will add inline notes to `annotations.md`:
- Corrections to assumptions
- Rejected approaches
- Domain knowledge you're missing
- Scope adjustments (removing nice-to-haves)

This cycle repeats 1-6 times until I approve.

## IMPORTANT
- DO NOT implement yet
- Wait for explicit "implement {TICKET}" command
- Each iteration, read annotations.md for my feedback
- Be specific about line numbers - vague plans fail
