# Workflow

## Add or change a binding

1. Is there a friction-log entry for it? If not, write one first.
2. Find the owner of the modifier in `modifier-ownership.md`. Wrong owner → pick another chord.
3. Edit `registry/<scope>.toml` (status `planned` → `active` once applied).
4. `scripts/kebo check` — must report zero new conflicts.
5. Apply in `configs/<tool>/` (symlinked into `$HOME`), reload the app.
6. `CHANGELOG.md`: what, why, revert.
7. Contract change? → ADR in `docs/decisions/`.

## Consult

| Need | Where |
| --- | --- |
| "What does X do?" / "How do I Y?" | `scripts/kebo find <query>` (fzf) or Raycast "kebo: find shortcut" |
| Overview / printable | `generated/cheatsheet.md` |
| Neovim leader tree | which-key popup (`<Space>` and wait) — always give maps a `desc` |
| Current keyboard layer | ZSA Keymapp (live layer view) or Oryx |

## Weekly review (15 min, same day every week)

1. Read new entries in `journal/friction-log.md`.
2. Pick the single most painful one. Decide: fix, defer, or drop.
3. Apply max 1–2 changes with the checklist above.
4. Review last week's changes: did they stick? If not, revert.
5. Update **Current status** in `PLAN.md`.

## Monthly prune

Bindings you never used in a month → `status = "deprecated"`. Next month → remove.
