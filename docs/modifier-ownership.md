# Modifier ownership (DRAFT — promote to ADR 0001 in Phase 2)

The anti-conflict contract. Each modifier namespace has exactly ONE owner.
A binding outside its owner's namespace is a defect that `kebo check` must flag.
Platform: macOS. Evidence: `inventory/2026-11-05-findings.md`.

## Interception order (outer wins)

```
Voyager firmware → macOS / Raycast → Ghostty → Herdr → shell / nvim / Claude Code / Pi / Gentle Shell
```

## Ownership table

| Namespace | Owner | Used for | Never used by |
| --- | --- | --- | --- |
| `Hyper` (⌃⌥⇧⌘) | Raycast | App switching, window management, global commands | Any app |
| `Meh` (⌃⌥⇧) | Raycast | Secondary global actions (clipboard, snippets, system) | Any app |
| `⌘ Space` | Raycast | Launcher (exception; Spotlight shortcut must be disabled) | — |
| `⌘ Cmd` (rest) | macOS + Ghostty | OS standards (copy/paste/quit) + Ghostty tabs/window | Terminal programs (they never receive it) |
| Prefix `⌃a` | Herdr | All Herdr commands (`prefix + key`) | — (shadows readline line-start: F2, ADR 0006) |
| `⌃⌥` (Ctrl+Alt) | Herdr | Optional direct chords (pane hjkl) — Herdr's documented safe family | Programs inside panes |
| `⌥ Alt` (whitelist, ADR 0007) | Terminal programs | Only `A-b/f/w/d/y/.` + `A-Enter`/`A-Backspace` | Herdr, Raycast |
| `⌃ Ctrl` | Terminal programs | Readline, nvim, Claude Code, Pi | Ghostty (except default `⌃Tab`), Raycast, Herdr (except prefix) |
| `Space` leader (normal mode) | Neovim | LazyVim leader tree | — |
| Option + `e n u i \` 1 ⇧/` | macOS input | Accents, ñ, ü, ¡, ¿ — both Option keys | Everything else |

## Rules

1. Ghostty binds only `Cmd` chords. It passes every `Ctrl` and `Alt` chord through.
2. Raycast binds only `Hyper` / `Meh` (plus the `Cmd+Space` launcher).
3. Herdr binds only `prefix + key` and, optionally, `Ctrl+Alt + key`. Never plain `Alt` (macOS composes it).
4. Terminal programs share `Ctrl`/`Alt` by **convention**: readline semantics
   (`C-a/e/w/u/k/y`, `A-b/f/d`) stay consistent across zsh, Claude Code, Pi and Gentle Shell.
5. Legacy terminal aliases are reserved: `C-i`=Tab, `C-[`=Esc, `C-m`=Enter, `C-h`=Backspace,
   `C-j`=newline (Pi uses it for new line).
6. A new namespace (e.g. a new app) requires an ADR.

## Open

- ADR 0006: Herdr prefix. Keep `⌃a` + move "line start" to `Home` on the Voyager Nav layer,
  or change prefix. Every candidate has an owner (`⌃b` cursor-left, `⌃Space` LazyVim selection).
- Ghostty splits: recommendation is NOT to use them — one split system (Herdr) is enough.
