# Configs

Real config files, versioned here and symlinked into `$HOME` (`scripts/kebo link`, Phase 5).
Move a tool here only when you start aligning it — not before.

| Folder | Target in `$HOME` (verify in Phase 1) | Notes |
| --- | --- | --- |
| `ghostty/` | `~/.config/ghostty/config` | Cmd-only keybinds, `macos-option-as-alt` |
| `nvim/` | `~/.config/nvim/lua/config/keymaps.lua` | Only the keymaps overlay, not all of LazyVim |
| `zsh/` | sourced from `~/.zshrc` | `keybindings.zsh` only |
| `herdr/` | TBD | Verify config location/format |
| `claude-code/` | `~/.claude/keybindings.json` | Verify support in installed version |
| `gentle-shell/` | `~/.pi/agent/keybindings.json` | Verify support in installed version |
| `raycast/` | not file-based | Keep `.rayconfig` export + registry as truth |
| `voyager/` | Oryx (cloud) | Layout URL, revision id, exported source |
