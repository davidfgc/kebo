# kebo

Personal keyboard + shortcut system for a terminal-first, vim-minded workflow.
One contract, one registry, many apps — no conflicts, easy to consult, easy to evolve.

## Stack

| Layer | Tool | Role |
| --- | --- | --- |
| Hardware | ZSA Voyager (split, home-row mods) | Layers, modifiers, nav |
| OS | macOS + Raycast | Global launcher, windows, Hyper keys |
| Terminal | Ghostty | Tabs/splits, key encoding to apps |
| Multiplexer | Herdr | Panes/workspaces for agent sessions |
| Apps | Neovim (LazyVim), zsh, Claude Code, Gentle Shell | Daily work |

## Resume in 60 seconds

1. Open `PLAN.md` → read **Current status** and **Next action**.
2. Skim `docs/modifier-ownership.md` (the contract that prevents conflicts).
3. Check `journal/friction-log.md` for open pains.
4. Working with an AI agent? It reads `AGENTS.md` automatically.

## Layout

```
kebo/
├── README.md              # you are here
├── PLAN.md                # roadmap, phases, current status, next action
├── AGENTS.md              # rules for AI agents (CLAUDE.md -> AGENTS.md)
├── CHANGELOG.md           # every binding change, newest first
├── docs/
│   ├── principles.md          # the philosophy (vim grammar, ownership)
│   ├── modifier-ownership.md  # WHO owns WHICH modifier (anti-conflict contract)
│   ├── keyboard-layers.md     # Voyager layers and home-row-mod tuning
│   ├── workflow.md            # add/change a binding, consult, review ritual
│   └── decisions/             # ADRs: why each contract choice was made
├── registry/              # single source of truth for every binding (TOML)
├── configs/               # real config files, symlinked into $HOME
├── inventory/             # read-only snapshots of the "before" state
├── journal/               # friction log + weekly reviews
├── scripts/               # check conflicts, generate cheatsheet, search
└── generated/             # build output (cheatsheet) — never edit by hand
```

## The three loops

- **Consult**: `generated/cheatsheet.md`, `scripts/kebo find <query>` (fzf), Raycast script command, LazyVim which-key.
- **Maintain**: change registry → `scripts/kebo check` → apply config → CHANGELOG.
- **Improve**: log friction when it happens → weekly 15-min review → at most 1–2 binding changes per week.
