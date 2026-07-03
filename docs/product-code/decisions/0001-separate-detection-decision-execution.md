---
domain: product-code
type: decision-record
status: accepted
owner: maintainer
supersedes:
---

# Separate detection, decision, and execution into independent stages

## Context

The obvious way to build a cleanup tool is a single script that deletes
anything untouched for N days. That's also exactly the kind of tool that
eventually deletes something it shouldn't have — and once an automated
deletion tool does that, it gets uninstalled, and trust doesn't come back.

Archiving a project is irreversible in the cases that matter most (an
unpushed commit is gone for good), but the *evidence* that a project is
stale — last-modified timestamps, git status, running containers — is easy
to gather automatically and cheap to get wrong. Conflating "notice this
looks stale" with "therefore remove it" means a false positive in detection
directly causes data loss.

## Decision

Detection, decision, and execution are three independent stages. Detection
(the scanner) only observes and reports — it has no ability to remove
anything. Decision is never automated — a human always has to look at a
specific finding and explicitly say yes before anything happens. Execution
only runs after that yes, and only after a tiered set of safety checks:
checks guarding against something unrecoverable block unconditionally,
while checks guarding against something merely inconvenient can be
knowingly overridden by the person making the decision.

## Consequences

- No archival action can ever be triggered by the scanner alone, even if its detection logic has a bug — the human-decision stage is a hard gate, not a convenience.
- This makes the tool slower than a fully automated cleanup script by design; the loss of pure automation is treated as the correct trade for making the tool trustworthy enough to actually keep running.
- Safety checks need to be classified by severity (unconditional vs. overridable) rather than implemented as a single uniform pass/fail gate — this adds design and maintenance surface that a single-script approach wouldn't have.
- Pre-existing debris (state that predates the tool) doesn't fit this loop cleanly, since detection confidence is lower there — it's handled as a separate, one-time pass rather than forced through the same three stages.

## Superseded by

<!-- Leave empty. Never edit an accepted decision — a change means a new file that supersedes this one. -->
