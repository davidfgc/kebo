# Registry (source of truth)

One TOML file per scope: `os.toml` (macOS/Raycast), `keyboard.toml`, `ghostty.toml`,
`herdr.toml`, `zsh.toml`, `nvim.toml`, `claude-code.toml`, `gentle-shell.toml`.

TOML because Python 3.11+ reads it with the stdlib (`tomllib`): zero dependencies for scripts.

## Schema (draft — finalize in Phase 3)

```toml
[[binding]]
id      = "nav.window.left"      # unique, dot-separated: <domain>.<object>.<verb>
scope   = "nvim"                 # owner tool (must match the file)
layer   = "app"                  # firmware | os | terminal | multiplexer | app
mode    = "normal"               # tool-specific mode, "" if none
keys    = "C-h"                  # notation: C- Ctrl, A- Alt, D- Cmd, S- Shift, Hyper-, Meh-
action  = "Focus window left"    # human description (shown in cheatsheet/search)
tags    = ["navigation", "hjkl"]
origin  = "default"              # default | custom
status  = "active"               # planned | active | deprecated
note    = ""                     # optional: why, conflicts, links to ADR
```

## Checks `kebo check` will run

1. **Duplicate**: same `keys` + `scope` + `mode` with different actions.
2. **Shadowing**: a chord bound in an outer layer that an inner layer also binds.
3. **Ownership**: the chord's modifier is not owned by the binding's scope.
4. **Reserved aliases**: `C-i`, `C-[`, `C-m`, `C-h` used as distinct bindings.
