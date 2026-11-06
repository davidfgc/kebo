# CHANGELOG

Newest first. One entry per binding change: what, why, how to revert.

## 2026-11-06
- Ghostty: add `alt+w=esc:f` (vim-style alias of forward-word; `alt+f` kept, prune monthly if unused). Shadows zsh `M-w` copy-region-as-kill (unused). Revert: delete the line. Note: Ghostty has no inline comments — a trailing `# ...` becomes part of the value.
- F3 / ADR 0007: Ghostty `macos-option-as-alt = false` + Alt whitelist `alt+b/f/d/y/.` → `esc:X`. Accents (Option+e/n/u/i/`/1, ¿) untouched. Revert: delete those lines from `~/.config/ghostty/config`.
- Removed empty duplicate Ghostty config `~/Library/Application Support/com.mitchellh.ghostty/config.ghostty` (0 bytes). Single source: `~/.config/ghostty/config`. Revert: `touch` the file.
- Fix F1: `~/.config/ghostty/config` line 1 stray prefix `9oˆ˚≥≤0p.` removed; `font-family` now applies (`+validate-config` clean). Revert: none needed (previous content in `inventory/ghostty/2026-11-05-config.txt`).

## 2026-11-05
- Inventory (read-only): Ghostty, nvim, Pi, Gentle Shell, Herdr. Findings F1–F7. No bindings changed.
- Contract draft: Herdr moves from plain `Alt` to prefix + optional `Ctrl+Alt`; `Alt` returns to terminal programs.
- Bootstrap: project scaffold, plan, draft contract. No bindings changed yet.
