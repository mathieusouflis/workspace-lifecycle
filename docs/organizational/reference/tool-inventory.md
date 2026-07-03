---
domain: organizational
type: reference
status: active
owner: maintainer
last_reviewed:
---

# Tool Inventory

Every external tool, dependency, or vendor this project relies on. Add a row here in the same PR that introduces a new one — this is the entry most commonly forgotten.

| Tool | Used for | Alternatives considered |
|---|---|---|
| GitHub | Source control, CI/CD, issue tracking | — |
| devenv / Nix | Reproducible local dev shell | — |
| Terraform (`integrations/github` provider) | Managing this repo's GitHub settings (branch protection, environments) as code | Manual Settings-tab configuration |

## See also

- [product-code/decisions](../../product-code/decisions/) — why a given tool was chosen over alternatives
- [.github/CODEOWNERS](../../../.github/CODEOWNERS) — per-path ownership (GitHub-native, kept at its required path)
