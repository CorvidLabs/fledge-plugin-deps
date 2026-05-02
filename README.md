# fledge-plugin-deps

Cross-ecosystem dependency health for [fledge](https://github.com/CorvidLabs/fledge) — `outdated`, `audit`, `licenses` against Rust, Node (npm/pnpm/yarn/bun), and Python (poetry/uv) projects.

Lived in fledge core through v0.14. Moved to this plugin as part of the v0.15 tight-core refactor — every additional ecosystem is one more lockfile parser core didn't need.

## Install

```sh
fledge plugins install CorvidLabs/fledge-plugin-deps
```

## Commands

### `fledge deps [--outdated | --audit | --licenses] [--json]`

Auto-detects the project ecosystem from lockfiles in the current directory, then shells out to the canonical tool:

| Lockfile | Ecosystem | Backing tool |
|----------|-----------|--------------|
| `Cargo.lock` | Rust | `cargo outdated` / `cargo audit` |
| `bun.lockb` | Node (Bun) | `bun outdated` / `bun audit` |
| `pnpm-lock.yaml` | Node (pnpm) | `pnpm outdated` / `pnpm audit` |
| `package-lock.json` | Node (npm) | `npm outdated` / `npm audit` |
| `yarn.lock` | Node (Yarn) | `yarn outdated` / `yarn npm audit` |
| `poetry.lock` | Python (Poetry) | `poetry show --outdated` / `pip-audit` |
| `uv.lock` | Python (uv) | `uv pip list --outdated` / `pip-audit` |

```sh
fledge deps --outdated
fledge deps --audit
```

Default action when no flag is set is `--outdated`.

## Why a plugin?

Every ecosystem has its own lockfile parser, registry API, and audit tooling. Adding Dart? Another parser. Adding Elixir? Another parser. As a plugin, this can grow ecosystem support independently — and a Rust-only shop never carries the npm/pip/swift code in their fledge binary.

## License

MIT
