# Symphony

Symphony is my personal, AI-native delegation system. It lets me operate more like a tech lead orchestrating a small team — setting direction, reviewing work, making key decisions — while offloading the grunt work of planning and building.

_Inspired by the excellent [Compounding Engineering Plugin](https://github.com/EveryInc/compounding-engineering-plugin) by Every, but adapted to my own needs and working style._

## Core values

- **No AI slop:** Succinct docs. Clean code. Output must meet my quality bar always.
- **Human-in-the-loop:** I review, decide, and course-correct. Can easily move up or down the stack depending on what we're working on.
- **Self-improving:** The system learns and adapts to my taste over time.
- **Fast feedback loops:** I know quickly if something's working or needs intervention, and making improvements to the system is low-friction.

## Installation

Add the plugin to Claude Code:

```bash
/plugin add /path/to/symphony/plugins/symphony
```

Or if publishing to a marketplace:

```bash
/plugin install symphony
```

## Dependencies

Currently relies on using Linear via MCP for issue tracking. I've been trying [beads](https://github.com/steveyegge/beads?tab=readme-ov-file) but I don't like having issue-tracking coupled with version control.

## Commands

| Command     | Description                                             |
| ----------- | ------------------------------------------------------- |
| `/plan`     | Turn a seed idea into a PRD in your preferred format    |
| `/work`     | Execute a plan in small steps, producing clean PRs      |
| `/review`   | Surface high-signal questions and risks for code review |
| `/compound` | Self-improvement—collect and propose system updates     |

## Status

This is an early scaffold. Many pieces are intentionally stubbed and will evolve through use.

- Commands exist but have minimal behavior
- Agents, skills, and MCP servers are not yet defined
- The system will grow as patterns emerge from real usage

## Project structure

```
plugins/symphony/
├── .claude-plugin/
│   └── plugin.json       # Plugin manifest
├── agents/               # Specialized agents (stubbed)
│   ├── review/
│   ├── workflow/
│   ├── docs/
│   └── research/
├── commands/
│   ├── workflows/        # Core commands (plan, work, review, compound)
│   └── utility/          # Helper commands (future)
├── skills/               # Reusable capabilities (future)
├── CLAUDE.md             # Plugin guidance
└── CHANGELOG.md          # Version history
```
