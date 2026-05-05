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
fledge deps --outdated --json
```

Default action when no flag is set is `--outdated`.

Pass `--json` to wrap the output in a JSON envelope (useful for piping into other tools or CI scripts).

> **Note:** `--licenses` is planned but not yet implemented.

## Requirements

The plugin auto-detects the ecosystem from lockfiles and shells out to the
corresponding tool. You need the backing tools installed for your ecosystem:

- **Rust:** `cargo-outdated` and/or `cargo-audit` (`cargo install cargo-outdated cargo-audit`)
- **Node:** `npm`, `pnpm`, `yarn`, or `bun` (whichever matches your lockfile)
- **Python:** `poetry` or `uv`, plus `pip-audit` for security audits (`pipx install pip-audit`)

## Why a plugin?

Every ecosystem has its own lockfile parser, registry API, and audit tooling. Adding Dart? Another parser. Adding Elixir? Another parser. As a plugin, this can grow ecosystem support independently — and a Rust-only shop never carries the npm/pip/swift code in their fledge binary.

## License

MIT
