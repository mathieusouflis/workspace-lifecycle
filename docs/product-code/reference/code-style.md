---
domain: product-code
type: reference
owner: maintainer
last_reviewed:
---

# Code Style Guide

This document defines the code style and formatting conventions for this project. Consistency matters more than any individual rule — when in doubt, follow existing patterns in the codebase.

---

## Tooling

```bash
# Check for style/lint errors
cargo fmt --check
cargo clippy --all-targets --all-features -- -D warnings

# Auto-fix formatting
cargo fmt
```

All checks must pass before a PR can be merged. The CI pipeline enforces this automatically — see [operations/concept/ci-cd-pipeline](../../operations/concept/ci-cd-pipeline.md).

---

## General Principles

- **Clarity over cleverness** — write code for the next reader, not the compiler
- **Explicit over implicit** — avoid magic; name things for what they do
- **Small functions** — each function should do one thing
- **No dead code** — remove commented-out code before committing; let `clippy` catch genuinely unused code rather than `#[allow(dead_code)]`-ing it away

---

## Naming Conventions

Standard Rust conventions, enforced by `clippy::style`:

| Element | Convention | Example |
|---------|------------|---------|
| Files / modules | `snake_case` | `project_scanner.rs` |
| Types (`struct`/`enum`/`trait`) | `UpperCamelCase` | `ScanResult` |
| Functions / methods / variables | `snake_case` | `find_stale_projects` |
| Constants / statics | `SCREAMING_SNAKE_CASE` | `MAX_SCAN_DEPTH` |
| Type parameters | short `UpperCamelCase` | `T`, `E` |

---

## Formatting

Enforced entirely by `rustfmt` with its default settings (`cargo fmt`) — no hand-formatting, no bikeshedding indentation or line length individually. A `rustfmt.toml` at the repo root can override defaults if a real need comes up; none exists yet.

---

## Import / Dependency Order

`rustfmt` groups and sorts `use` statements automatically. Convention within a module:

1. `std`
2. External crates
3. Crate-internal (`crate::`, `super::`, `self::`)

---

## Error Handling

- Library code returns `Result<T, E>` with a typed, structured error (e.g. via `thiserror`) — never swallow an error silently
- Application/binary code may use `anyhow` at the boundary to add context and propagate to `main`
- No `.unwrap()`/`.expect()` outside of tests and cases already proven infallible by a preceding check
- Validate inputs at system boundaries (CLI args, filesystem/process state read from the OS); trust internal invariants elsewhere

---

## Testing Conventions

- Unit tests live in the same file as the code they test, under `#[cfg(test)] mod tests`
- Integration tests (exercising the built CLI end-to-end) live in `tests/`
- Each test should be independent and not rely on shared mutable state or execution order
- Test names describe the expected behavior: `returns_paused_when_project_untouched_for_threshold`

---

## Running the Full Validation Suite

```bash
cargo fmt --check
cargo clippy --all-targets --all-features -- -D warnings
cargo test
cargo build --release
```

All four must pass before pushing.

## See also

- [operations/concept/ci-cd-pipeline](../../operations/concept/ci-cd-pipeline.md) — how these checks run in CI
- [product-code/tutorials/getting-started](../tutorials/getting-started.md)
