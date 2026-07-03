# workspace-lifecycle

[![CI](https://github.com/mathieusouflis/workspace-lifecycle/actions/workflows/ci.yml/badge.svg)](https://github.com/mathieusouflis/workspace-lifecycle/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A CLI that manages the lifecycle of local development projects: it scans for
projects that have gone stale, lets you decide what to do about each one, and
only archives a project once a set of safety checks confirms it's actually
safe to lose. It also sets up new projects with self-contained, isolated
dependencies from day one, so nothing leaks into the rest of the machine for
archiving to clean up later.

---

## Table of Contents

- [Overview](#overview)
- [Getting Started](#getting-started)
- [Architecture](#architecture)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

Development machines accumulate state faster than anyone cleans it up — stale
projects, orphaned containers, global packages nobody remembers installing.
`workspace-lifecycle` splits the fix into three separate stages: a scanner
**notices** what's gone stale, you **decide** what to do about it, and only
after that decision does the tool **execute** it — never automatically.
Archiving (the one irreversible step) only happens once a set of safety
checks confirms it's actually safe, with stricter checks for anything
unrecoverable and softer, overridable checks for anything merely
inconvenient. New projects also start fully isolated (no global package/tool
leakage), so there's nothing left over for archiving to clean up later.

---

## Getting Started

```bash
git clone https://github.com/mathieusouflis/workspace-lifecycle.git
cd workspace-lifecycle
./bin/mat setup   # Git hooks, .env, dev shell (Nix/direnv/devenv), repo config
```

On native Windows (no WSL2), run `.\bin\mat.ps1` instead.

Full setup guide (prerequisites, dependency install, dev server): [docs/product-code/tutorials/getting-started](docs/product-code/tutorials/getting-started.md).

---

## Architecture

The tool is built around three separate stages — detection, decision, and
execution — kept deliberately independent so an irreversible action (archiving
a project) can never happen without an explicit human decision in between.
See [docs/product-code/concept/architecture-overview](docs/product-code/concept/architecture-overview.md) for the full breakdown and [docs/product-code/decisions/0001-separate-detection-decision-execution](docs/product-code/decisions/0001-separate-detection-decision-execution.md) for why.

```
.
├── src/           # Source code (Rust)
├── docs/          # Documentation — organized by domain × type, see docs/README.md
└── .github/       # GitHub configuration
```

---

## Documentation

All project documentation lives in [`docs/`](docs/README.md), organized by domain (what it's about) × type (what shape it takes). Start there for anything beyond this quickstart — architecture, environment variables, coding conventions, CI/CD, decisions, and more.

---

## Contributing

Contributions are welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a pull request.

---

## License

Distributed under the [MIT License](LICENSE).
