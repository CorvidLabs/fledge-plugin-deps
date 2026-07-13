---
spec: deps.spec.md
---

## User Stories

- As a developer, I want one dependency-health command across supported ecosystems.
- As an automation author, I want machine-readable ecosystem and output fields.

## Acceptance Criteria

### REQ-deps-001

The plugin SHALL detect Rust, Bun, pnpm, npm, Yarn, Poetry, and uv projects from their lockfiles in deterministic order.

### REQ-deps-002

The plugin SHALL run outdated by default and support an explicit security audit action.

### REQ-deps-003

The plugin SHALL report missing backing tools with installation guidance and exit 127.

### REQ-deps-004

JSON mode SHALL emit the detected ecosystem and safely escaped command output.

### REQ-deps-005

The unimplemented licenses action SHALL fail before running ecosystem tooling.

## Constraints

- The corresponding ecosystem command must be installed and usable in the project.

## Out of Scope

- Installing tools, parsing lockfiles directly, and license reporting until implemented.
