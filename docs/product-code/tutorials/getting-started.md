---
domain: product-code
type: tutorial
owner: maintainer
last_reviewed:
---

# Getting Started

This guide walks a new contributor from zero to a running local environment. It assumes no prior context — for a specific task you already know how to do (e.g. "add an endpoint"), see [product-code/reference](../reference/) instead.

---

## Prerequisites

| Tool | Version | Install |
|------|---------|---------|
| Rust (via `rustup`) | stable, latest | https://rustup.rs |

Everything else (git, gh, terraform, jq, shellcheck, shfmt) is provided by the reproducible dev shell (`devenv`/Nix) set up by `./bin/mat setup`.

---

## Setup

1. **Clone the repository**

   ```bash
   git clone https://github.com/mathieusouflis/workspace-lifecycle.git
   cd workspace-lifecycle
   ```

2. **Activate the Git hooks** (one-time, after cloning)

   ```bash
   git config core.hooksPath .githooks
   ```

   Details: [team-process/how-to/activate-git-hooks](../../team-process/how-to/activate-git-hooks.md).

3. **Copy the environment file**

   ```bash
   cp .env.example .env
   ```

   `workspace-lifecycle` has no environment variables yet — see [product-code/reference/environment-variables](../reference/environment-variables.md).

4. **Install dependencies**

   ```bash
   cargo build
   ```

5. **Run the CLI**

   ```bash
   cargo run -- --help
   ```

---

## Common Commands

```bash
cargo run -- <args>                                        # Run the CLI
cargo test                                                 # Run tests
cargo clippy --all-targets --all-features -- -D warnings   # Run linter
cargo build --release                                      # Build for production
```

---

## Troubleshooting

**Dependencies not installing / build fails**

Make sure `rustup show` reports a toolchain matching [Prerequisites](#prerequisites). Delete `Cargo.lock` and re-run `cargo build` to rule out a stale lockfile.

**Tests fail locally but pass in CI (or vice versa)**

Reinstall dependencies from the lockfile (`cargo build --locked`) to rule out local drift.

**Build fails with errors you didn't introduce**

Pull the latest `main` and rebuild — a dependency may have been updated since your last build.

For anything else, open an [issue](../../../../issues).

## See also

- [product-code/reference/environment-variables](../reference/environment-variables.md)
- [team-process/how-to/activate-git-hooks](../../team-process/how-to/activate-git-hooks.md)
