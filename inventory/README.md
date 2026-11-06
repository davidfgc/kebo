# Inventory (read-only snapshots)

Snapshots of the real state, one folder per tool, dated: `inventory/<tool>/YYYY-MM-DD-*`.
Never edit a snapshot; take a new one.

## Phase 1 capture commands (run yourself, or allow an agent per path)

```sh
D=$(date +%F)
mkdir -p inventory/{ghostty,nvim,zsh,raycast,voyager,herdr,claude-code,gentle-shell}

# Ghostty: config, default keybinds, validation
cp ~/.config/ghostty/config "inventory/ghostty/$D-config.txt"
ghostty +list-keybinds --default > "inventory/ghostty/$D-default-keybinds.txt"
ghostty +validate-config > "inventory/ghostty/$D-validate.txt" 2>&1

# Neovim: every mapping with origin (force VeryLazy so LazyVim keymaps load headless)
nvim --headless -c 'lua vim.api.nvim_exec_autocmds("User",{pattern="VeryLazy"})' \
  -c 'redir! > /tmp/kebo-maps.txt | silent verbose nmap | silent verbose xmap | silent verbose imap | redir END' -c 'qa!'
cp /tmp/kebo-maps.txt "inventory/nvim/$D-maps.txt"

# Herdr: config + `herdr config check`; defaults from the config reference of YOUR version:
# https://raw.githubusercontent.com/herdrdev/herdr/v<version>/docs/next/website/src/data/config-reference.json
cp ~/.config/herdr/config.toml "inventory/herdr/$D-config.toml"

# Pi / Gentle Shell: custom file if any; defaults live in the package docs/keybindings.md
ls ~/.pi/agent/keybindings.json ~/.gentle-shell/agent/keybindings.json

# zsh: active keymap bindings
zsh -ic 'bindkey -L' > "inventory/zsh/$D-bindkey.txt"
```

Manual captures:
- **Raycast**: Settings → Extensions → list hotkeys (or Settings → Advanced → Export).
- **Voyager**: Oryx layout URL + revision; download source if available.
- **Herdr / Claude Code / Gentle Shell**: copy keybinding config if it exists; otherwise note defaults from docs/help.

After capture: write pains and conflicts in `journal/friction-log.md`.
