# Implementation Phase

## Core Principle
Execute the approved plan without interruption. Trust the plan - it's been reviewed.

## Prerequisites
- Plan has been approved (I said "implement {TICKET}")
- All annotation cycles are complete
- No open questions remain

## Instructions

### 1. Load Context
- Read `~/boris/workstreams/{TICKET}/plan.md`
- Read `~/boris/workstreams/{TICKET}/annotations.md`
- Note any final corrections

### 2. Execute Completely
- Follow the plan exactly as approved
- Make changes in the specified order
- Run typecheck/compile after each file
- Fix issues before proceeding
- Do NOT ask for confirmation mid-execution

### 3. Track Progress
Update `~/boris/workstreams/{TICKET}/progress.md` as you go:
- Mark tasks complete immediately after finishing
- Note any deviations from plan
- Log blockers if encountered

### 4. Commit Strategy
- Commit incrementally with descriptive messages
- Include ticket ID: "TICKET-123: Description"
- Group related changes logically

### 5. Handle My Feedback
During implementation, my feedback will be terse:
- Single sentences
- Screenshots
- Brief corrections

This is intentional - you have full context from the plan.

## Output

Keep `~/boris/workstreams/{TICKET}/progress.md` updated:

```markdown
# Progress: {TICKET}

## Status: IN_PROGRESS | COMPLETED | BLOCKED

## Completed
- [x] Task 1 (commit abc123)
- [x] Task 2 (commit def456)

## In Progress
- [ ] Task 3 (current)

## Remaining
- [ ] Task 4
- [ ] Task 5

## Commits
- abc123: Description
- def456: Description

## Deviations
- None / List any changes from approved plan

## Blockers
- None / List any issues
```

## IMPORTANT
- Proceed without interruption
- Trust the approved plan
- Only stop if truly blocked
- Keep session continuous (don't split across conversations)
