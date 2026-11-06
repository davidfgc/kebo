# Principles

## 1. Vim grammar everywhere

Bindings are a language, not a list. Reuse the same verbs and directions:

| Concept | Key | Applies to |
| --- | --- | --- |
| Directions | `h j k l` | arrows (Nav layer), windows, panes, splits, OS windows |
| Next / previous | `n` / `p` (or `]` / `[`) | tabs, buffers, results, hunks |
| Close / quit | `x` / `q` | pane / app-level |
| Search | `/` | in-app search, command palettes |
| New | `t` (tab), `s`/`v` (split horizontal/vertical) | Ghostty, Herdr, nvim |

## 2. Same keys, different scope = different modifier

The direction keys never change; the **modifier selects the scope** (outer → inner):

```
Hyper     + hjkl → OS windows       (Raycast)
prefix    + hjkl → Herdr panes      (Herdr default)
Ctrl+Alt  + hjkl → Herdr panes      (optional direct chord, Herdr's recommended family)
Ctrl      + hjkl → Neovim windows   (LazyVim default)
Nav layer   hjkl → arrow keys       (Voyager)
```

Learn one motion, use it at every depth. Ghostty splits are intentionally left out:
one split system (Herdr) is enough.

## 3. One owner per modifier

Outer layers intercept keys before inner layers see them (OS → Ghostty → Herdr → app).
If two layers want the same chord, the outer one silently wins and the inner one breaks.
So every modifier namespace has exactly one owner. See `modifier-ownership.md`.

## 4. Home row first, thumbs second, reach last

- Frequent actions live on the home row (via home-row mods or layers).
- Thumbs hold layers and the highest-frequency keys (Space, Esc, Enter, Backspace).
- Number row and corners are for rare actions.

## 5. Defaults over customization

Prefer the tool's default if it already fits the grammar (e.g. LazyVim `<C-hjkl>`).
Every custom binding is a maintenance cost. Remap only to resolve a conflict or a measured pain.

## 6. Change slowly, measure honestly

- Max 1–2 binding changes per week.
- A change exists to fix an entry in the friction log. No entry, no change.
- Revert without shame if it does not stick after two weeks.
