# Symphony Plugin

## Core values

These values guide all behavior in this plugin:

1. **No AI slop** — Output must meet Dan's quality bar. Generic, over-engineered, or soulless code is unacceptable.

2. **Human-in-the-loop** — Dan reviews, decides, and course-corrects. The system surfaces questions and proposals; it doesn't make autonomous decisions.

3. **Self-improving** — The system should learn and adapt over time. Capture patterns, collect feedback, and propose improvements.

4. **Fast feedback loops** — If something takes too long to set up or produces garbage, it's not worth it. Optimize for quick iteration.

## Current status

This plugin is scaffolded but not yet fully implemented.

- **Commands:** Exist with placeholder workflows. Fill in behavior as patterns emerge.
- **Agents:** Directories exist but no agents are defined yet. Add agents that encode specific review criteria, planning patterns, etc.
- **Skills:** Not yet defined. Add skills when you feel the pain for reusable capabilities.

## Versioning

When making changes:

1. Bump version in `.claude-plugin/plugin.json` (semver)
2. Update `CHANGELOG.md` with what changed
3. Keep this file updated if core values or structure change

## Directory structure

```
agents/
├── review/     # Code review agents
├── workflow/   # Work orchestration agents
├── docs/       # Planning and documentation agents
└── research/   # Codebase and external research agents

commands/
├── workflows/  # Core commands (plan, work, review, compound)
└── utility/    # Helper commands

skills/         # Reusable capabilities (future)
```

## Adding new components

### To add an agent

1. Create `agents/<category>/<agent-name>.md`
2. Define the agent's role, expertise, and behavior
3. Reference it from commands using `Task agent-name(...)`

### To add a skill

1. Create `skills/<skill-name>/SKILL.md`
2. Define what the skill does and how to invoke it
3. Reference it from commands/agents using `skill: skill-name`

### To add a command

1. Create `commands/<category>/<command-name>.md`
2. Add frontmatter with `name`, `description`, `argument-hint`
3. Define the workflow in the body

