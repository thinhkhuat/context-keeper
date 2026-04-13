# Product Context

## Project Overview
ConKeeper (context-keeper) — file-based agent memory system for AI coding assistants. Replaces database-backed context with plain Markdown files in `.claude/memory/`. Multi-platform: Claude Code, Copilot, Codex, Cursor, Windsurf, Zed.

## Architecture
- **Hooks (Bash):** session-start, user-prompt-submit, post-tool-use, pre-compact, stop — all in `hooks/`
- **Skills:** memory-init, memory-sync, memory-search, memory-reflect, memory-insights, memory-config, session-handoff — in `skills/`
- **Commands:** Slash commands wrapping skills — in `commands/`
- **Tools:** CLI scripts (memory-search.sh, install.sh, build.sh) — in `tools/`
- **Storage:** Flat `.md` files + YAML frontmatter config. No database.
- **Shared libs:** `lib-config.sh` (YAML parsing), `lib-privacy.sh` (private block stripping), `lib-handoff.sh` (lifecycle automation)
- **Test suite:** 16 phases (phase-03 through phase-16) + functional integration tests

## Key Stakeholders
- **Upstream:** swannysec (single maintainer)
- **Fork:** thinhkhuat — for dogfooding and worktree-based multi-agent workflow

## Constraints
- Bash 3.2 compatible (macOS system bash) — no associative arrays, mapfile, etc.
- Zero runtime dependencies (jq/bc optional, graceful degradation if missing)
- Apache-2.0 + Commons Clause license

## Non-Goals
- Not a database replacement — intentional flat-file design
- Not a vector search engine — grep/ripgrep only
- Not a team sync solution (yet)

---
*Last updated: 2026-04-14 by Pi*
