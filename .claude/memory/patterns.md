# Project Patterns

## Code Conventions
- Bash 3.2 compatible — no associative arrays, mapfile, readarray
- `set -euo pipefail` in all scripts
- ERR trap exits 0 (fail-open) in hooks, non-zero in tools
- Symlink escape prevention: `[ -L "$file" ]` checks before every read/write
- JSON encoding: jq preferred, pure-bash fallback
- Config via YAML frontmatter in `.memory-config.md`, parsed by `lib-config.sh`

## Architecture Patterns
- Hook → lib → output pattern: hooks source shared libs, emit JSON
- Progressive disclosure: token budget gates control what's injected
- Privacy enforcement at every code path (search, sync, reflect, injection)
- Graceful degradation: every dependency (jq, bc, git) has fallback path

## Testing Patterns
- 16-phase test suite in `tests/phase-NN-*`
- Functional integration tests in `tests/functional/`
- Tests create temp dirs, setup mock git repos, run hooks, assert JSON output

---
*Last updated: 2026-04-14*
