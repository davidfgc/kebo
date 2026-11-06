# Voyager layers (DRAFT — promote to ADR 0003 in Phase 2)

ZSA Voyager: 52 keys, 2 thumb keys per hand. Alpha layout: QWERTY (non-goal to change).

## Layers

| # | Layer | Activation | Content |
| --- | --- | --- | --- |
| 0 | Base | default | QWERTY + home-row mods |
| 1 | Nav | hold thumb (Space side) | Right: `hjkl` = ←↓↑→, `y/o` = Home/End, `u/i` = PgDn/PgUp. Left: one-shot mods |
| 2 | Sym | hold thumb (other side) | Programming symbols, brackets paired on mirrored keys |
| 3 | Num | hold Sym + Nav, or dedicated thumb | Numpad on right hand, F-keys on left |
| 4 | System | combo / rare | Media, brightness, mouse keys, firmware reset |

## Thumb keys (proposal)

| Hand | Inner thumb | Outer thumb |
| --- | --- | --- |
| Left | `Esc` (tap) / Sym (hold) | `Backspace` (tap) / Num (hold) |
| Right | `Space` (tap) / Nav (hold) | `Enter` (tap) / Hyper (hold) |

`Esc` on a thumb is the single biggest win for vim + Claude Code (Esc interrupts agents).

## Home-row mods (proposal, mirrored on both hands)

| Finger | Left | Right | Modifier |
| --- | --- | --- | --- |
| Pinky | `a` | `;` | ⌘ Cmd |
| Ring | `s` | `l` | ⌥ Alt |
| Middle | `d` | `k` | ⌃ Ctrl |
| Index | `f` | `j` | ⇧ Shift |

Why: `Ctrl` is the hottest modifier in a terminal, so it gets the strong middle finger.
Mirrored mods mean you always press mod and key with **opposite hands** (`C-d` = right-middle + `d`).

## Misfire control (verify availability in Oryx for your firmware)

- **Chordal hold** (opposite-hand rule): same-hand rolls resolve as taps.
- **Flow tap**: fast typing streams never trigger mods.
- Tapping term: start ~200 ms, adjust per finger (pinky slower) only if misfires are logged.
- If Oryx lacks a feature you need → ADR 0004 (QMK userspace).
