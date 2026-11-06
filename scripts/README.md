# Scripts (Phase 3)

Single entry point `scripts/kebo`, Python 3.11+ stdlib only.

| Command | Does |
| --- | --- |
| `kebo check` | Validate registry: duplicates, shadowing, ownership, reserved aliases. Non-zero exit on conflict. |
| `kebo cheatsheet` | Render `generated/cheatsheet.md` grouped by scope and tag. |
| `kebo find [query]` | fzf over all bindings: `keys │ scope │ action`. |
| `kebo link` | Symlink `configs/*` into `$HOME` (backs up existing files first, dry-run by default). |

Not implemented yet — build in Phase 3, test-first, one command at a time.
