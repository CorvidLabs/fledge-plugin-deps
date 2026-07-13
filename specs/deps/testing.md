---
spec: deps.spec.md
---

## Test Plan

### Integration Tests

- `shellcheck bin/fledge-deps`
- `bin/fledge-deps --help`
- Verify `--licenses` returns the documented failure without ecosystem tooling.
