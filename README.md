# Boris Workflow

A structured three-phase approach to AI-assisted development. Never let Claude write code until you've reviewed and approved a written plan.

Based on: https://boristane.com/blog/how-i-use-claude-code/

## Setup

1. Add reference to your `~/.claude/CLAUDE.md`:
   ```markdown
   # Personal Workflow

   See `~/boris/CLAUDE.md` for Boris workflow commands.
   ```

2. Clone this repo to `~/boris/`

3. Add `workstreams/` to `.gitignore` to keep your work private

## Quick Reference

| Command | Purpose |
|---------|---------|
| `boris help` | Show workflow diagram and all commands |
| `boris init {TICKET}` | Initialize a new workstream |
| `boris research {TICKET} - {description}` | Phase 1: Deep codebase exploration |
| `boris plan {TICKET}` | Phase 2: Create implementation plan |
| `boris implement {TICKET}` | Phase 3: Execute approved plan |
| `boris switch {TICKET}` | Resume a workstream |
| `boris status` | Show all workstreams and their status |

## Status Flow

```
INITIALIZED → RESEARCH_COMPLETE → PLAN_READY → IN_PROGRESS → COMPLETED
                                      ↑______________|
                                   (annotation cycles)
```

## Directory Structure

```
~/boris/
├── CLAUDE.md                    # Workflow commands (Claude reads this)
├── README.md                    # This file
├── prompts/                     # Templates (shared with team)
│   ├── research.md              # How to do research
│   ├── plan.md                  # How to create plans
│   └── implement.md             # How to implement
└── workstreams/                 # Per-ticket work (personal, not committed)
    └── {TICKET}/
        ├── research.md          # Findings from codebase exploration
        ├── plan.md              # Implementation plan with code snippets
        ├── annotations.md       # YOUR review notes (you edit this)
        └── progress.md          # Status and todo tracking
```

## Key Concepts

| File | Who writes | Purpose |
|------|------------|---------|
| `prompts/*.md` | You (once) | Instructions for Claude - HOW to work |
| `workstreams/{TICKET}/*.md` | Claude | Work artifacts - WHAT was done |
| `annotations.md` | You | Feedback and corrections for Claude |

## Key Principles

1. **Separation of phases** - Research → Plan → Implement, never skip
2. **Written artifacts** - All findings/plans go to files for review
3. **Annotation cycles** - You add notes, Claude incorporates them
4. **Reference implementations** - Find similar patterns before proposing
5. **Scope control** - You trim nice-to-haves, Claude implements what's approved
6. **Single sessions** - Keep research, planning, implementation in one conversation
7. **Next steps** - Always show what command to run next

---

## Example Walkthrough: CORE-2478

### Step 1: Initialize

```
You: boris init CORE-2478
```

Claude creates:
```
~/boris/workstreams/CORE-2478/
├── research.md
├── plan.md
├── annotations.md
└── progress.md
```

Output: "Workstream initialized. Next: `boris research CORE-2478`"

---

### Step 2: Research

```
You: boris research CORE-2478 - Fix ArrayIndexOutOfBoundsException in
     EncryptionProviderImpl.decryptData() when empty ciphertext is passed.
     Stack trace shows error at checkEncodedCipherVersion() line 43.
```

Claude:
1. Reads `~/boris/prompts/research.md` for instructions
2. Deeply explores the codebase
3. Writes findings to `~/boris/workstreams/CORE-2478/research.md`

Output: "Research complete. Review `research.md`, add notes to `annotations.md`, then: `boris plan CORE-2478`"

---

### Step 3: Your Review (Annotations)

You open `~/boris/workstreams/CORE-2478/annotations.md` and add:

```markdown
# Annotations: CORE-2478

## Review Notes

### After Research
- For decryptData: empty ciphertext should return empty byte[], not throw
- For encryptData: null should throw, empty should encrypt (valid use case)
- Yes, add checks to both methods
- Log warning with keySpecId and keyIdentifier
- Use BnContext pattern for structured logging
```

---

### Step 4: Plan

```
You: boris plan CORE-2478
```

Claude:
1. Reads research.md + annotations.md
2. Creates detailed plan in `~/boris/workstreams/CORE-2478/plan.md`

Output: "Plan ready. Review `plan.md`, add notes to `annotations.md`. Then either:
- `boris plan CORE-2478` - revise plan with your feedback
- `boris implement CORE-2478` - execute approved plan"

---

### Step 5: Your Review (More Annotations)

You add to annotations.md:

```markdown
### After Plan v1
- Plan looks good, approved
- Make sure to use withContext() not withValue() for logging
```

---

### Step 6: Implement

```
You: boris implement CORE-2478
```

Claude:
1. Reads plan.md + annotations.md
2. Executes each change
3. Runs compile after each file
4. Updates progress.md
5. Commits with descriptive messages

Output: "Implementation complete. Next: create PR or `boris status` to see all workstreams"

---

## Tips

1. **Be specific in research prompts** - Include error messages, stack traces, file paths
2. **Use annotations liberally** - Correct assumptions, reject approaches, add domain knowledge
3. **Iterate on plans** - Run `boris plan` multiple times until satisfied
4. **Keep sessions continuous** - Don't split research/plan/implement across conversations
5. **Terse feedback during implement** - Single sentences are fine, Claude has full context

---

## Templates

### ~/boris/workstreams/{TICKET}/progress.md

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
