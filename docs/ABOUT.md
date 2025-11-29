# Conductor

_Personal delegation system for orchestrating AI agents_

## Mission

Build a delegation system that lets me operate more like a tech lead orchestrating a small team - setting direction, reviewing work, making key decisions - while offloading the grunt work of planning and building, so I can apply my judgment and taste to more things without drowning in execution details or producing garbage code.

## Core Values & Constraints

- **No AI slop**: The output has to meet my quality bar - this is non-negotiable because my whole value prop is taste
- **Keeps me in the loop**: I'm not trying to disappear - I still want to review, make decisions, course-correct. Just not write every line or plan every detail
- **Increases surface area**: The point is I can work on more things simultaneously (Relay + side project + Corner) without feeling scattered or like I'm making linear progress
- **Fast feedback loops**: If delegating to an agent takes 30 minutes to plan, it's not worth it. I need to know quickly if something's working or needs my intervention. Focus on finding friction points and reducing them.
- **Self-improving**: The system should learn and adapt to my personal taste over time - my specific preferences for code style, architecture decisions, what constitutes "done", etc. This becomes part of my highly customized personal toolkit.

## System Shape

A Claude Code plugin with commands + sub-agents, similar to Compounding Engineering but built for my own tastes.

## Agent Principles

### High Signal Only

Surface non-obvious problems, not obvious ones. Good questions expose system interactions, downstream effects, or gaps in the plan that would require a decision. Bad questions are generic concerns ('what about error handling?'), style preferences, or things with standard answers. If an experienced engineer would handle it automatically, don't ask about it. If it would make Dan pause and think 'oh shit, I didn't consider that,' ask about it.

## Commands

### /plan

Take a kernel of an idea (with as much or as little detail as I feel is necessary) and flesh it out into a PRD in a format that makes sense to me.

**Current pain points with existing tools:**

- Docs are too long, too much to read
- Not broken effectively into small tasks
- Not easily editable depending on which tool I'm using

**Features:**

- T-shirt sizing (SM project has different format than XL project)
- Standard formatting
- End goal: I love love love using this tool to plan without any of the friction I feel with other tools

#### Linear Workflow

Use Linear MCP server for issue tracking. Keeps docs + task management outside of git to avoid staleness/sync issues with gitworktrees.

**Size-based structure:**

- **SM**: Single task (no sub-tasks)
- **MD**: Task + sub-tasks (2-7 sub-tasks)
- **LG**: Project with tasks (TBD - save for later)

**Breadcrumbs:**

- Every sub-task description includes "See parent ticket for full context"
- Agent instructions: Always check parent ticket when working on a sub-task
- Ensures context flows through the whole chain

#### Small Mode

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

Agent can immediately pick up the task and start working.

#### Medium Template

```markdown
# [Project Title]

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

### /work

Pick up a Linear ticket (already planned with full context), write the code, commit, and open a PR for review.

**Workflow:**

1. Pick up Linear ticket (context from planning is already there)
2. Write code following engineering guidelines
3. Build and test locally
4. Commit the work
5. Open PR following PR template
6. Display PR URL for review

**Engineering Guidelines:**

- **Ship what's asked for, nothing more.** Don't implement features that weren't requested. Don't add "nice to have" improvements. Stick to the ticket.
- **Readable over clever.** When in doubt, ask: could a junior engineer read this? Optimize for clarity, not showing off.
- **No unnecessary abstractions.** Don't create frameworks for one use case. Don't add layers of indirection "for future flexibility." Build what's needed now. **If you're considering adding an abstraction or new pattern, flag it for review** - the orchestrating engineer may have context about future work that makes it worthwhile.
- **Standard patterns.** Use the patterns already established in the codebase. **If you need to introduce a new pattern or deviate from existing ones, call it out in the PR** - explain why the existing approach doesn't work and get confirmation before merging.
- **Defer to project standards.** Run formatting, linting, testing as directed by the project's own instructions. Don't reinvent these.

**PR Structure:**

Titles:

- Sentence case (not Title Case)
- Descriptive and specific - clearly explain what the PR does
- Use action verbs (Fix, Add, Update, Remove, etc.)
- Include Linear ticket reference if applicable (e.g. "LIN-123: Fix provider schedule analysis")

Descriptions:

- Keep it short and readable - easy to scan
- Start with "This PR" followed by 1-3 sentences about what it accomplishes
- Use active voice over passive voice
- For multi-part changes, use bullet lists
- Optionally add context in a separate paragraph if needed

**PR Template:**

```markdown
This PR [clearly describes what the PR accomplishes in 1-3 sentences using active voice].

[Optional: Additional context paragraph if needed - explain why this approach was taken, note future work, provide context for future code spelunkers]

## Needs Attention

[High-signal items for review - only include if there are noteworthy items:

- System interactions or downstream effects
- Architectural decisions made (especially new patterns or abstractions)
- Edge cases or constraints that required judgment calls
- Dependencies or assumptions

Skip this section entirely if there's nothing noteworthy - don't manufacture concerns.]

Closes [Linear ticket link]
```

**Example PRs:**

Good: "Add appointment status change logging"

- Description: "This PR adds logging for appointment status changes so we can track when and why appointments move between states."

Good: "CH-322: Migrate schedule analyzer from Interval to admin app"

- Description: "This PR migrates the schedule analyzer from Interval to the admin app. Preserves all existing functionality while moving to the new architecture. The migration will make it easier to maintain going forward."

Good: "Update claim flagging systems"

- Description: "This PR updates our claim flagging system with several improvements:
  - Marks some claims as 'persistent' so they aren't automatically removed between runs
  - Replaces 'add insufficient funds flag' action with general 'add flag' action
  - Supports adding flags from Charge Copays and Charge Cash Appointments tools
  - Removes unused code"

**Features:**

- Issue tracking via Linear
- Sequential work support (stacked PRs when needed)
- Well-structured PRs that surface high-signal review items

### /review

Explore how I could delegate code review to AI.

**Key insight:** If I use AI to plan, another agent to work, and feed the output into a code review agent - what might it look like if the review agent says "whoa, you really over-built this - dan, did he overbuild it?"

**Inspiration:**

- OpenAI Codex code reviews at work are SUPER effective at calling out really subtle bugs I would otherwise miss
- Gut-check stuff that helps surface high-signal issues

**Note:** The human has to be in the loop SOMEWHERE - this is about surfacing the right questions/concerns, not replacing judgment

### /review

Review a PR and surface high-signal issues before the human does their review. Acts as a gut-check to catch things that might be missed.

**Focus areas:**

- Overbuilding - did the agent implement more than what was asked?
- Subtle bugs - edge cases, off-by-one errors, race conditions, etc.
- System interactions - downstream effects or breaking changes
- Missed requirements from the Linear ticket

**Output:**

If no issues found:

- Thumbs up the GitHub PR
- Leave a comment: "Looks good to me"
- Minimal noise

If issues found:

- Leave a comment with 1-2 paragraph summary:
  - What the issue is
  - Why it's a problem
  - How to potentially solve it
- Focus on actionable feedback, not stylistic preferences

**Philosophy:**
Apply the "high signal only" principle - surface non-obvious problems that would make the orchestrating engineer say "good catch," not obvious things an experienced engineer would handle automatically. The human still does the final review and makes all decisions.

### /compound

The self-improvement component - make this a self-improving system.

**Possible features:**

- Recommending new agents to add
- Updates to docs, style guides, templates, etc.
- "Agent mail" system where agents write notes to each other in a file
- System keeps track of notes and has tools for incorporating suggested improvements
- /compound reads the mail + captures what to improve

**Status:** Most open-ended - research project to figure out the best format

## Next Steps

Start ridiculously small. Pick one annoying repeated task and build something that handles just that one thing in a way that actually matches how I think. Don't try to build the whole system yet.

Timebox exploration to ~1 hour every Saturday morning, see what emerges.

## Meta Notes

This is an experiment to see if I can work this way. Might discover it feels terrible or that the overhead is worse than doing it myself. Or might discover I'm actually pretty good at it and it unlocks a new gear.

Building this skill also helps prepare for senior roles where I'll need to be comfortable reviewing code and guiding work rather than always being hands-on-keyboard.
