# 0007 — Option composes; whitelisted chords act as Alt (Ghostty)

- Status: accepted (pending manual check)
- Date: 2026-11-06

## Context
Finding F3: `Option+b/f` typed `∫ƒ` instead of readline word motions in Ghostty.
The owner types accents with Option using **opposite hands**: right Option + `e` (´),
left Option + `n` (˜). Both Option keys are needed for writing — and Spanish is typed
in the terminal constantly (prompts to coding agents).

## Decision
In `~/.config/ghostty/config`:
- `macos-option-as-alt = false` (explicit; unset depends on the active keyboard layout).
- Only these chords are translated to Alt via `keybind = alt+X=esc:X`:
  `b` (word back), `f` (word forward), `w` (alias of `f`, vim-style — added 2026-11-06),
  `d` (delete next word), `y` (yank-pop), `.` (last argument).
- `alt+w` sends `M-f` to every program in Ghostty; it shadows zsh `M-w` (copy-region-as-kill, unused).
  Readline forward-word stops at word END (vim `e`), not word start (vim `w`). Accepted.
- Reserved for typing, never bound: `alt+e`, `alt+n`, `alt+u`, `alt+i`, ``alt+` ``, `alt+1`, `alt+shift+/`.
- Option+Enter / Option+Backspace need nothing: they print no character, so Ghostty sends Alt.

Verified in Ghostty 1.4 docs: codepoint triggers match the *unmodified* key plus modifiers,
so `alt+b` fires even when Option would compose `∫`.

## Alternatives considered
- `macos-option-as-alt = left` → breaks ñ (left Option + n).
- `macos-option-as-alt = right` → breaks accents (right Option + e).
- `true` → breaks both.
- US International / Spanish input source → makes `'` and `"` dead keys or moves symbols; bad for code.
- Accent macros on a Voyager layer → possible later, but retrains muscle memory for no gain now.

## Consequences
- Accents and ñ work as before, with both hands.
- Readline word motions work in zsh, Pi, Gentle Shell, Claude Code, Herdr fields.
- Any new Alt chord a terminal program needs must be added to the whitelist explicitly
  (check it is not a reserved accent key first).
