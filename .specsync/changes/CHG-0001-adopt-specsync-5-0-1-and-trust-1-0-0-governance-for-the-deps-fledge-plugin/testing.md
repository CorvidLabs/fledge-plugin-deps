---
change: CHG-0001-adopt-specsync-5-0-1-and-trust-1-0-0-governance-for-the-deps-fledge-plugin
artifact: testing
---

# Testing

- `shellcheck bin/fledge-deps`
- `bin/fledge-deps --help`
- `specsync check --strict --force` at advisory threshold 0
- `specsync agents status`
- `fledge trust doctor` and `fledge trust verify`
