---
domain: product-code
type: concept
owner: maintainer
last_reviewed:
---

# Architecture Overview

## The three stages

The tool is built around three components, kept deliberately independent so
that an irreversible action can never happen without an explicit human
decision in between:

| Stage | Responsibility |
|---|---|
| **Detection** (scanner) | Runs on its own schedule, inspects local projects and machine state (containers, global packages, build caches), and reports what it found. Never modifies anything. |
| **Decision** (you) | Nothing is ever removed without a human looking at the scanner's report and saying yes. This stage has no automation — it exists specifically to *not* be automated. |
| **Execution** (actions) | Runs only after an explicit yes, and only after a set of safety checks confirms the decision is actually safe to act on. |

## Data flow

1. The scanner walks known project roots and machine-wide state (containers, global package installs, caches) on a schedule.
2. Findings are classified into one of three project states — **active** (no action), **paused** (a soft, informational nudge), or a candidate for **archival** (the one irreversible step).
3. Archival candidates are presented to the user, never acted on automatically.
4. On confirmation, a set of safety checks runs before execution — checks guarding against something unrecoverable (e.g. an unpushed commit) block unconditionally; checks guarding against something merely inconvenient (e.g. a missing setup file) can be knowingly overridden.
5. Execution reduces the project to its most durable form: a remote repository plus a written record of what state existed and what happened at archive time. Restoring it afterward is a manual act, not an automated one.

## Isolation, from project creation onward

The other half of the system runs earlier in a project's life, not at
cleanup time: every new project starts with its dependencies fully
self-contained, so that nothing leaks into the rest of the machine for
archiving to have to clean up later. This also means switching into a
project can automatically load the right tools and versions, since the
environment is already self-contained.

## Key constraints that shaped the design

- **Trust is the scarce resource.** A tool that deletes the wrong thing once gets uninstalled — see [decisions/0001-separate-detection-decision-execution](../decisions/0001-separate-detection-decision-execution.md) for why detection, decision, and execution are separate stages rather than one pipeline.
- **Not all risk is equal.** Safety checks are tiered by the actual cost of being wrong, not treated as uniformly strict.
- **Pre-existing debris is handled once, separately.** State that predates the system (legacy containers, hand-installed tools) is a one-time pass, not folded into the ongoing scan/decide/execute loop, because confidence in what's safe to remove is lower for that category.

## See also

- [product-code/decisions](../decisions/) — individual architectural choices
- [product-code/reference](../reference/) — concrete CLI/config lookup
