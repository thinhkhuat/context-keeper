# ADR-001: Fork & Worktree-Based Multi-Agent Workflow

**Status:** Accepted | **Date:** 2026-04-14 | **Tags:** workflow, multi-agent, git-worktree

## Context
Solo dev using multiple coding agents (Pi, Claude Code, Codex, Kilo, Droid) on a few projects simultaneously, dozens of sessions per day. Need a memory system that works across all agents without collisions.

## Decision
Fork ConKeeper and use git worktree isolation — each agent gets its own worktree per task. Memory files (`.claude/memory/`) are isolated per worktree, eliminating concurrent write collisions. Memory propagates back via git merge.

## Rationale
- ConKeeper is the only tool that works across all 5+ agents (flat .md files = universal)
- Git worktrees solve the `.last-sync` stampede and `active-context.md` clobbering problems
- Memory merges cleanly via git (text files), unlike SQLite/ChromaDB (binary)
- No runtime dependencies to manage across different agent environments

## Consequences
- Positive: Zero collision risk, git-native memory history, works everywhere
- Negative: Memory is isolated per worktree — must merge branches to propagate context
- Neutral: Requires discipline to merge worktree branches regularly

## Alternatives Considered
- claude-mem: Claude-only, AGPL-3.0, requires SQLite+ChromaDB — rejected (single agent)
- ConPort: MCP-only, Python+ChromaDB — rejected (not all agents support MCP)
- Mem0: Cloud-based, SDK integration — rejected (privacy, per-agent integration cost)

## Superseded By
None
