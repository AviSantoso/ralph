# Ralph Agent Instructions

## Overview

Ralph is an autonomous AI agent loop that runs AI coding tools (Amp, Claude Code, or Codex) repeatedly until all PRD items are complete or the configured maximum iteration count is reached. Each iteration is a fresh instance with clean context, and each agent instance is allowed to complete at most one user story before stopping.

## Commands

```bash
# Run the flowchart dev server
cd flowchart && npm run dev

# Build the flowchart
cd flowchart && npm run build

# Run Ralph with Amp (default)
./ralph.sh [max_iterations]

# Run Ralph with Claude Code
./ralph.sh --tool claude [max_iterations]
```

## Key Files

- `ralph.sh` - The bash loop that spawns fresh AI instances (supports `--tool amp`, `--tool claude`, or `--tool codex`)
- `prompt.md` - Instructions given to each AMP instance
- `prompt-codex.md` - Instructions given to each Codex instance
- `CLAUDE.md` - Instructions given to each Claude Code instance
- `prd.json.example` - Example PRD format
- `flowchart/` - Interactive React Flow diagram explaining how Ralph works

## Flowchart

The `flowchart/` directory contains an interactive visualization built with React Flow. It's designed for presentations - click through to reveal each step with animations.

To run locally:
```bash
cd flowchart
npm install
npm run dev
```

## Patterns

- Each iteration spawns a fresh AI instance (Amp or Claude Code) with clean context
- Memory persists via git history, `progress.txt`, and `prd.json`
- Stories should be small enough to complete in one context window
- One agent iteration may complete only one story; finishing that story must end the agent session immediately
- Ralph decides whether to start another iteration; the agent does not decide whether the overall run continues
- A single `ralph.sh` invocation may run multiple iterations until the PRD is fully complete or max iterations are exhausted
- Always update AGENTS.md with discovered patterns for future iterations
