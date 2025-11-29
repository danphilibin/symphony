---
name: review
description: Review a PR and surface high-signal issues before the human does their review
argument-hint: "[PR number, URL, or branch]"
---

# Review Command

Review a PR and surface high-signal issues before the human does their review. Acts as a gut-check to catch things that might be missed.

## Focus Areas

- Overbuilding - did the agent implement more than what was asked?
- Subtle bugs - edge cases, off-by-one errors, race conditions, etc.
- System interactions - downstream effects or breaking changes
- Missed requirements from the Linear ticket

## Output

**If no issues found:**

- Thumbs up the GitHub PR
- Leave a comment: "Looks good to me"
- Minimal noise

**If issues found:**

- Leave a comment with 1-2 paragraph summary:
  - What the issue is
  - Why it's a problem
  - How to potentially solve it
- Focus on actionable feedback, not stylistic preferences

## Philosophy

Apply the "high signal only" principle - surface non-obvious problems that would make the orchestrating engineer say "good catch," not obvious things an experienced engineer would handle automatically. The human still does the final review and makes all decisions.
