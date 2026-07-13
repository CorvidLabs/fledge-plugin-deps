---
spec: deps.spec.md
---

## Context

This shell plugin moved cross-ecosystem dependency health out of fledge core while preserving the prior command surface.

## Related Modules

- fledge plugin command interface

## Design Decisions

- Delegate to canonical ecosystem tools instead of maintaining lockfile parsers.
- Fail unimplemented actions before side effects.
