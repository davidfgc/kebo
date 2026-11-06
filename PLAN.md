# PLAN

## Current status

- Phase: **1 — Inventory** (partial: Ghostty, nvim, Pi, Gentle Shell, Herdr done)
- Last updated: 2026-11-06
- Findings: `inventory/2026-11-05-findings.md` (F1–F7), pains in `journal/friction-log.md`
- Next action: manually verify ADR 0007 (`Option+b` / `Option+w` jump words, `Option+e e` = é, `Option+n n` = ñ)
  → decide F2 (Herdr prefix, ADR 0006). Then inventory Claude Code, zsh, Raycast, Voyager.

> Update this block at the end of every session. It is the resume point.

## Goals

1. **Efficiency** — fewer keystrokes, fewer hand movements, home row first.
2. **Standardization** — the same semantic key means the same thing in every app.
3. **No conflicts** — every modifier has exactly one owner (`docs/modifier-ownership.md`).
4. **Consultable** — any binding findable in < 5 seconds.
5. **Maintainable** — every change recorded, reversible, and explained.

## Non-goals

- Changing the alpha layout (QWERTY → Colemak/etc.) — out of scope unless an ADR says otherwise.
- Rebinding everything at once. Muscle memory is the asset; change it in small, deliberate steps.

## Phases

### Phase 0 — Bootstrap ✅
- [x] Project scaffold, README, AGENTS, PLAN, docs drafts
- [ ] `git init` + first commit (your call)

### Phase 1 — Inventory (read-only, no changes)
Goal: know the real "before" state and its conflicts.
- [x] Snapshot Ghostty config → `inventory/ghostty/`
- [x] Snapshot Neovim/LazyVim mappings (`:redir` of `:map`, custom `keymaps.lua`) → `inventory/nvim/`
- [ ] Snapshot zsh bindings (`bindkey -L`) → `inventory/zsh/`
- [ ] Snapshot Raycast hotkeys (manual list or `.rayconfig` export) → `inventory/raycast/`
- [ ] Snapshot Voyager layout (Oryx URL + revision, exported source) → `inventory/voyager/`
- [x] Snapshot Herdr keymap (prefix model, `ctrl+a`; defaults from v0.9.1 config reference) → `inventory/herdr/`
- [ ] Snapshot Claude Code keybindings (verify `~/.claude/keybindings.json`) → `inventory/claude-code/`
- [x] Snapshot Gentle Shell / Pi keybindings (no custom file; Pi defaults captured) → `inventory/pi/`, `inventory/gentle-shell/`
- [ ] Write top 10 pains + known conflicts in `journal/friction-log.md`
- Exit: every tool has a snapshot or a note saying why not.

### Phase 2 — Contract (decisions)
Goal: freeze the rules before touching configs.
- [ ] ADR 0001 — Modifier ownership (promote `docs/modifier-ownership.md` from draft)
- [ ] ADR 0002 — Directional grammar: hjkl everywhere, modifier = scope
- [ ] ADR 0003 — Voyager layers + home-row-mod order and timing
- [ ] ADR 0004 — Firmware source: Oryx vs QMK userspace
- [ ] ADR 0005 — Registry format (TOML) + tooling language (Python stdlib)
- [ ] ADR 0006 — Herdr prefix vs readline `Ctrl+a` (finding F2)
- [x] ADR 0007 — Option composes; whitelisted chords act as Alt (finding F3)
- Exit: ownership table has no "TBD" for modifiers you actually use.

### Phase 3 — Registry + tooling
Goal: one source of truth, machine-checked.
- [ ] Finalize schema in `registry/README.md`
- [ ] Populate `registry/<scope>.toml` from the inventory (status = active)
- [ ] `scripts/kebo check` — duplicates, shadowing, ownership violations
- [ ] `scripts/kebo cheatsheet` → `generated/cheatsheet.md`
- [ ] `scripts/kebo find` — fzf search over the registry
- [ ] Raycast script command wrapping `kebo find`
- Exit: `kebo check` passes on the current state (or lists known conflicts as planned fixes).

### Phase 4 — Keyboard (Voyager)
- [ ] Implement layers from `docs/keyboard-layers.md`
- [ ] Tune home-row mods (chordal hold / flow tap if available, tapping term)
- [ ] Export layout to `configs/voyager/` and record revision in CHANGELOG
- [ ] 2-week adaptation: daily 10 min practice, track misfires in friction log

### Phase 5 — Apps alignment (one app per iteration)
Order = outermost layer first, because outer layers shadow inner ones:
- [ ] Raycast (Hyper/Meh namespace)
- [ ] Ghostty (Cmd namespace only; pass Ctrl/Alt through; option-as-alt)
- [ ] Herdr (its namespace per contract)
- [ ] zsh (vi-mode or emacs readline — ADR)
- [ ] Neovim/LazyVim (leader + Ctrl-hjkl; every custom map with `desc`)
- [ ] Claude Code + Gentle Shell (align to the same semantics)
- [ ] Move each real config into `configs/` and symlink (`scripts/kebo link`)

### Phase 6 — Operate (forever)
- [ ] Weekly review ritual (`docs/workflow.md`)
- [ ] Monthly: prune unused bindings (status = deprecated → removed)

## Open questions (resolve in Phase 2)

- Herdr: does `Ctrl+a Ctrl+a` send a literal `Ctrl+a` to the pane? (not documented in 0.9.1 — test manually)
- zsh: vi-mode or keep emacs readline (Ctrl-a/e/w/r are shared with Claude Code and most REPLs)?
- Does Oryx expose chordal hold / flow tap for your firmware version, or is QMK userspace needed?
