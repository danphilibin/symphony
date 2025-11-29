---
name: work
description: Pick up a Linear ticket, write the code, commit, and open a PR for review
argument-hint: "[Linear ticket ID or URL]"
---

# Work Command

Pick up a Linear ticket (already planned with full context), write the code, commit, and open a PR for review.

## Workflow

1. Pick up Linear ticket (context from planning is already there)
2. Write code following engineering guidelines
3. Follow per-project guidelines for buliding, linting, testing, etc.
4. Commit the work
5. Open PR following PR template
6. Display PR URL for review

## Engineering Guidelines

- **Ship what's asked for, nothing more.** Don't implement features that weren't requested. Don't add "nice to have" improvements. Stick to the ticket.
- **Readable over clever.** When in doubt, ask: could a junior engineer read this? Optimize for clarity, not showing off.
- **No unnecessary abstractions.** Don't create frameworks for one use case. Don't add layers of indirection "for future flexibility." Build what's needed now. **If you're considering adding an abstraction or new pattern, flag it for review** - the orchestrating engineer may have context about future work that makes it worthwhile.
- **Standard patterns.** Use the patterns already established in the codebase. **If you need to introduce a new pattern or deviate from existing ones, call it out in the PR** - explain why the existing approach doesn't work and get confirmation before merging.
- **Defer to project standards.** Run formatting, linting, testing as directed by the project's own instructions. Don't reinvent these.

## PR Structure

**Titles:**

- Sentence case (not Title Case)
- Descriptive and specific - clearly explain what the PR does
- Use action verbs (Fix, Add, Update, Remove, etc.)
- Include Linear ticket reference if applicable (e.g. "LIN-123: Fix provider schedule analysis")

**Descriptions:**

- Keep it short and readable - easy to scan
- Start with "This PR" followed by 1-3 sentences about what it accomplishes
- Use active voice over passive voice
- For multi-part changes, use bullet lists
- Optionally add context in a separate paragraph if needed

## PR Template

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

Closes [Linear project identifier]
```
