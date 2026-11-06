# Instructions for AI agents

This repo is the owner's keyboard + shortcut system. You help design, check, and apply bindings.

## Read first (in order)

1. `PLAN.md` — current status and next action. Work on the next action unless told otherwise.
2. `docs/modifier-ownership.md` — the anti-conflict contract. It wins over any suggestion.
3. `docs/principles.md` — vim grammar and design rules.
4. `journal/friction-log.md` — open pains are the backlog.

## Hard rules

- **Registry first.** Never change an app config without the matching change in `registry/`.
  The registry is the source of truth; configs and cheatsheets derive from it.
- **Respect ownership.** A binding that uses a modifier owned by another scope is a defect.
  If the user asks for one, explain the conflict and propose an alternative, or propose an ADR.
- **Small steps.** At most 1–2 binding changes per session unless the user asks for more.
  Muscle memory is expensive to retrain.
- **No silent writes outside this repo.** Ask before reading or writing anything in `$HOME`
  (e.g. `~/.config/ghostty`, `~/.config/nvim`, `~/.claude`). Name the exact path.
- **`inventory/` is read-only history.** Never edit snapshots; add a new dated one instead.
- **`generated/` is build output.** Never edit by hand.
- **Ghostty config has no inline comments.** `keybind = x=y  # note` makes `# note` part of the
  value. Put comments on their own line; check with `ghostty +show-config`.
- **Verify, don't assume.** Tool keymap models (Herdr, Claude Code, Gentle Shell, Oryx features)
  change between versions. Check the installed version's docs before relying on a feature.

## Change checklist (every binding change)

1. Update `registry/<scope>.toml`.
2. Run `scripts/kebo check` (once it exists) — zero new conflicts.
3. Apply to `configs/<tool>/`.
4. Add an entry to `CHANGELOG.md` (what, why, how to revert).
5. If it changes the contract → new ADR in `docs/decisions/`.
6. Update **Current status** in `PLAN.md` at the end of the session.

## Language

Repository artifacts are in English. Talk to the owner in the language they use.
