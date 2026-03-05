# Boris Workflow Commands

Based on Boris Tane's three-phase approach: never let Claude write code until you've reviewed and approved a written plan.

Reference: https://boristane.com/blog/how-i-use-claude-code/

## Workstream Commands

### boris init {TICKET}
Initialize a new workstream with all files:
1. Create `~/boris/workstreams/{TICKET}/` directory
2. Create initialized files:
   - `~/boris/workstreams/{TICKET}/research.md` - with template for findings
   - `~/boris/workstreams/{TICKET}/plan.md` - with template for implementation plan
   - `~/boris/workstreams/{TICKET}/annotations.md` - empty, for my review notes
   - `~/boris/workstreams/{TICKET}/progress.md` - with status template and todo checklist
3. **Show next step:** "Workstream initialized. Next: `boris research {TICKET}`"

### boris research {TICKET}
Phase 1 - Deep exploration (no code):
1. Read `~/boris/prompts/research.md` for instructions
2. Deeply analyze the codebase - use "deeply", "intricacies", "in great detail"
3. Find reference implementations (similar patterns in codebase)
4. Write findings to `~/boris/workstreams/{TICKET}/research.md`
5. Update `progress.md` status to RESEARCH_COMPLETE
6. **DO NOT write any code**
7. **DO NOT propose solutions**
8. **Show next step:** "Research complete. Review `research.md`, add notes to `annotations.md`, then: `boris plan {TICKET}`"

### boris plan {TICKET}
Phase 2 - Iterative planning (no code):
1. Read `~/boris/workstreams/{TICKET}/research.md`
2. Read `~/boris/workstreams/{TICKET}/annotations.md` for my feedback
3. Create detailed plan based on reference implementations found
4. Include specific file paths, line numbers, code snippets
5. Write to `~/boris/workstreams/{TICKET}/plan.md`
6. Update `progress.md` status to PLAN_READY
7. **DO NOT implement yet**
8. **Show next step:** "Plan ready. Review `plan.md`, add notes to `annotations.md`. Then either:
   - `boris plan {TICKET}` - revise plan with your feedback
   - `boris implement {TICKET}` - execute approved plan"

### boris implement {TICKET}
Phase 3 - Execute approved plan:
1. Read `~/boris/workstreams/{TICKET}/plan.md`
2. Read `~/boris/workstreams/{TICKET}/annotations.md`
3. Update `progress.md` status to IN_PROGRESS
4. Execute the plan without interruption
5. Track completed tasks in `progress.md`
6. Run typecheck/compile after each file change
7. Commit incrementally with ticket ID in message
8. Update `progress.md` status to COMPLETED when done
9. **Show next step:** "Implementation complete. Next: create PR or `boris status` to see all workstreams"

### boris switch {TICKET}
Resume a workstream:
1. Read all files in `~/boris/workstreams/{TICKET}/`
2. Summarize current state and where we left off
3. **Show next step** based on current status in `progress.md`

### boris status
Show all workstreams:
1. List directories in `~/boris/workstreams/`
2. Show status from each `progress.md`
3. **Show available commands** for each workstream based on status

### boris help
Show workflow overview:
1. Display the status flow diagram
2. List all available commands with brief descriptions
3. Show key principles

## Status Flow

```
INITIALIZED → RESEARCH_COMPLETE → PLAN_READY → IN_PROGRESS → COMPLETED
                                      ↑______________|
                                   (annotation cycles)
```

## ~/boris/workstreams/{TICKET}/progress.md Template

```markdown
# Progress: {TICKET}

## Status: INITIALIZED

## Completed
(none yet)

## In Progress
(none yet)

## Remaining
- [ ] Research codebase
- [ ] Create implementation plan
- [ ] Implement approved plan
- [ ] Create PR

## Commits
(none yet)

## Deviations
(none yet)

## Blockers
(none)
```

## Key Principles

1. **Separation of phases** - Research → Plan → Implement, never skip
2. **Written artifacts** - All findings/plans go to files for review
3. **Annotation cycles** - I add inline notes, you incorporate them
4. **Reference implementations** - Find similar patterns before proposing
5. **Scope control** - I trim nice-to-haves, you implement what's approved
6. **Single sessions** - Keep research, planning, implementation in one conversation
7. **Next steps** - Always show what command to run next
