---
module: deps
version: 1
status: active
files:
  - bin/fledge-deps

db_tables: []
depends_on: []
---

# Deps

## Purpose

Detect Rust, Bun, pnpm, npm, Yarn, Poetry, or uv projects from lockfiles and invoke their canonical outdated or security-audit tools, with optional JSON wrapping.

## Public API

| Option | Behavior |
|--------|----------|
| outdated | Run the selected ecosystem's outdated-dependency command; this is the default action. |
| audit | Run the selected ecosystem's security-audit command. |
| licenses | Fail fast with the documented not-implemented status. |
| JSON | Wrap detected ecosystem and escaped command output in JSON. |

## Invariants

1. Lockfile detection uses a deterministic precedence: Cargo, Bun, pnpm, npm, Yarn, Poetry, then uv.
2. No action flag defaults to outdated.
3. Licenses fails before detecting an ecosystem or running a tool.
4. Missing required backing tools report installation guidance and exit 127.
5. JSON output escapes backslashes, quotes, and newlines.
6. Bun audit may fall back to npm only after Bun audit fails.

## Behavioral Examples

```
Given both `bun.lock` and `package-lock.json`
When dependency health runs without an explicit action
Then Bun is selected and its outdated command runs
```

## Error Cases

| Error | When | Behavior |
|-------|------|----------|
| Unknown argument | Unsupported CLI input | Report it and exit 64. |
| Unknown ecosystem | No recognized lockfile | List checked lockfiles and exit 65. |
| Unimplemented licenses | Licenses is requested | Report not implemented and exit 70. |
| Missing backing tool | Required command is absent | Report installation guidance and exit 127. |

## Dependencies

- Bash plus sed and awk for JSON escaping
- ecosystem-native Cargo, Bun, pnpm, npm, Yarn, Poetry, uv, and pip-audit tools as selected

## Change Log

| Version | Date | Changes |
|---------|------|---------|
| 1 | 2026-07-12 | Document existing dependency detection and command behavior for SpecSync 5 adoption. |
