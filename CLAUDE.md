# Claude Code Operating Instructions

You are working inside a structured content automation repository.

## High-Level Goals
- Build agent-based, repeatable content workflows
- Support multiple brands (Amplify Intelligence, Houston AI Club)
- Prioritize architecture, orchestration, and correctness over speed

## Critical Rules
- Do NOT generate final blog or social content unless explicitly requested
- Always propose a plan before implementing major changes
- Prefer reusing existing agents, skills, and commands
- Keep changes minimal, composable, and easy to explain

## Repository Conventions
- `.claude/agents` = specialized workers
- `.claude/commands` = orchestrated workflows
- `.claude/skills` = reusable logic modules
- `context/` = all brand and global reference material
- `drafts/` = generated but unpublished outputs

## Brand Architecture
- All brand-specific context lives under `context/brands/{brand-name}/`
- Agents must never hardcode brand assumptions
- Commands should accept a `--brand` parameter when applicable

## Development Approach
- Implement features in small, testable phases
- Show file diffs and explain changes
- Avoid speculative features unless asked

## Default Mode
- Plan mode first
- Then implement in small commits
