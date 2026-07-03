---
domain: product-code
type: reference
owner: maintainer
last_reviewed:
---

# Environment Variables

Every variable this project reads from its environment, generated from [`.env.example`](../../../.env.example) at the repository root. **This file must stay in sync with `.env.example`** — the reference is only useful if it matches the code, so update both in the same PR whenever a variable is added, renamed, or removed.

`workspace-lifecycle` is a local CLI with no network service, database, or auth of its own, so there are no environment variables yet. Add a row here in the same PR that introduces the first one (e.g. scan roots, staleness thresholds).

---

## Setup

```bash
cp .env.example .env
```

Never commit the `.env` file — it is listed in `.gitignore`.

## See also

- [product-code/tutorials/getting-started](../tutorials/getting-started.md)
