---
id: CHG-0001-adopt-specsync-5-0-1-and-trust-1-0-0-governance-for-the-deps-fledge-plugin
state: implementing
type: migration
base_commit: b8b902ceda32936bf43ffb4cdf19fb59340c1dbc
---

# Adopt SpecSync 5.0.1 and Trust 1.0.0 governance for the Deps Fledge plugin

## Intent

Adopt SpecSync 5.0.1 and Trust 1.0.0 governance for the Deps Fledge plugin

## Affected Canonical Specs

- None

## Acceptance Criteria

- SpecSync strict check passes at explicit advisory threshold 0; all four integrations report installed; Trust doctor and verification pass; ShellCheck and help smoke remain green

## No-spec Rationale

The migration documents existing Deps behavior and adds governance configuration without changing runtime semantics.
