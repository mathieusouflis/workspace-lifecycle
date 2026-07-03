# Documentation

Organized by two axes: **domain** (what this document is about) and **type** (what shape it takes / what the reader is trying to do). A document always lives at the intersection of both — e.g. `product-code/reference/` is a lookup table about the code, `team-process/how-to/` is a step-by-step guide about how the team works.

| Type → <br> Domain ↓ | Concept | How-to | Reference | Decisions | Tutorials | Runbooks |
|---|---|---|---|---|---|---|
| **[product-code](product-code/)** | [Architecture overview](product-code/concept/architecture-overview.md) | — | [Code style](product-code/reference/code-style.md), [Environment variables](product-code/reference/environment-variables.md) | [0001 — Separate detection/decision/execution](product-code/decisions/0001-separate-detection-decision-execution.md) | [Getting started](product-code/tutorials/getting-started.md) | — |
| **[operations](operations/)** | [CI/CD pipeline](operations/concept/ci-cd-pipeline.md), [Repository configuration](operations/concept/repository-configuration.md) | — | — | — | — | [Deployment](operations/runbooks/todo_deployment-runbook.md) 🚧 |
| **[team-process](team-process/)** | — | [Activate Git hooks](team-process/how-to/activate-git-hooks.md) | [Commit conventions & PR process](../CONTRIBUTING.md) ⧉ | — | — | — |
| **[organizational](organizational/)** | — | — | [Tool inventory](organizational/reference/tool-inventory.md), [Code owners](../.github/CODEOWNERS) ⧉ | — | — | — |

🚧 = template placeholder (`todo_` prefix), no real content yet — see the note inside each file for what to fill in and how to rename it once done. The deployment runbook stays a placeholder deliberately: no deployment target has been decided for this CLI tool yet.
⧉ = lives outside `docs/` at a fixed path, see below.

This project has a single maintainer, so `organizational/concept/` (role charter) and the org-level `decisions/` folder (tooling choice) were dropped entirely — there's no team boundary to charter and no separate org-level decision-maker from the product-code one. `tool-inventory` stays as a plain lookup table with no per-row "owner" column.

A few things intentionally live outside this grid, at fixed paths GitHub itself expects: [`README.md`](../README.md), [`CONTRIBUTING.md`](../CONTRIBUTING.md), [`CODE_OF_CONDUCT.md`](../CODE_OF_CONDUCT.md), [`SECURITY.md`](../SECURITY.md), [`LICENSE`](../LICENSE), and [`.github/CODEOWNERS`](../.github/CODEOWNERS). Moving them would break the platform features tied to those paths (Security tab, community profile checklist, the PR-open banner) — so unlike the rest of the grid, these stay canonical at their GitHub-required location, and the grid links *to* them rather than absorbing their content. `CONTRIBUTING.md` in particular is intentionally kept complete (commit conventions, bug/feature reporting, PR process included inline) rather than split into `docs/team-process/`, since GitHub surfaces it directly at the moment a contributor opens a PR or issue — splitting it would add a click at exactly the point someone needs the answer fastest.
