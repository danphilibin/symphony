---
name: plan
description: Take a kernel of an idea and flesh it out into a PRD in Linear
argument-hint: "[idea or feature description]"
---

# Plan Command

Take a kernel of an idea (with as much or as little detail as I feel is necessary) and flesh it out into a PRD of appropriate size, length, and detail for the scale of the project.

Do NOT work on the tasks, just complete the "plan" step as described below.

Use Linear MCP server for issue tracking.

## Size-based structure

Projects have three "size modes" that expect different output depending on project size:

- **SM**: Single task (no sub-tasks)
- **MD**: Task + sub-tasks (2-7 sub-tasks)
- **LG**: Project with tasks (TBD - save for later)

If using sub-tasks, every sub-task description should include "See parent ticket for full context".

## Small Mode

Zero friction from input → Linear task → agent working → PR open.

**Input:** 1-2 sentences from Dan, optionally success criteria
**Process:** Minimal transformation - just create the Linear task
**Output:** Single Linear task (no sub-tasks)

**Linear task fields:**

- **Title:** Generated from input - sentence case, succinct, clearly describes the work
- **Description:** Dan's input (lightly cleaned up if needed) + success criteria if provided
- No breadcrumbs needed (standalone task)

**Examples:**

- Input: "Add dark mode toggle to settings page"
- Input: "Fix the bug where users can't upload PDFs larger than 10MB. Should work up to 50MB."
- Input: "Refactor the auth middleware to use the new session store"

Include enough context that an agent can immediately pick up the task and start working.

## Medium Template

```markdown
# [Project title - sentence case]

## Context

[Current behavior, intended behavior, technical and/or business context. Should always be clear WHY we are doing this work. Keep it tight - 2-4 sentences for simple projects, up to 1-3 paragraphs for more complex ones. Use judgment. This context will flow into PR descriptions.]

## Tasks

[Think in terms of Linear tickets - discrete, sequential pieces of work that can be assigned and tracked individually.]

### 1. [Task Title - sentence case, succinct]

**What**: [Description of the work - could be a sentence or bullets depending on complexity]

### 2. [Next task...]

[Repeat structure]

## Open Questions

[Only include if there are genuine blockers or architectural decisions needed. Should be specific and answerable. Skip generic "how should we handle X" questions. What would a tech lead need to know?]

## Success Criteria

- [Concrete, testable outcomes - what "done" looks like]
- [Keep to 2-4 items max]

## Non-Goals

- [What we're explicitly NOT doing in this iteration]
- [Helps prevent scope creep and overbuilding]
```
