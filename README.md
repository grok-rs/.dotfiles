# Dotfiles

Personal dotfiles for a Wayland/Sway Linux development environment, managed with [GNU Stow](https://www.gnu.org/software/stow/).

## What's Included

| Tool | Config | Purpose |
|------|--------|---------|
| [Sway](https://swaywm.org/) | `sway/` | Tiling Wayland compositor |
| [Waybar](https://github.com/Alexays/Waybar) | `waybar/` | Status bar |
| [Neovim](https://neovim.io/) | `nvim/` | Editor (LazyVim + Catppuccin) |
| [Neovide](https://neovide.dev/) | `neovide/` | Neovim GUI |
| [Zed](https://zed.dev/) | `zed/` | Editor (alternative) |
| [Tmux](https://github.com/tmux/tmux) | `tmux/` | Terminal multiplexer |
| [Zsh](https://www.zsh.org/) | `zsh/` | Shell (Oh My Zsh + P10k) |
| Custom scripts | `bin/` | tmux-sessionizer, etc. |

## Quick Start

```bash
# Clone
git clone --recursive git@github.com:grok-rs/.dotfiles.git ~/.dotfiles

# Install
cd ~/.dotfiles
./bootstrap
```

## Prerequisites

Install these before running bootstrap:

```bash
# Core
sudo apt install git stow zsh curl

# Desktop
sudo apt install sway waybar rofi grim slurp wl-clipboard brightnessctl

# Terminal & editors
sudo apt install kitty tmux neovim

# Dev tools
sudo apt install fzf ripgrep fd-find build-essential
```

### Additional setup

- **Oh My Zsh**: `sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`
- **Powerlevel10k**: `git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k`
- **zsh-autosuggestions**: `git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions`
- **alias-tips**: `git clone https://github.com/djui/alias-tips.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/alias-tips`
- **Neovide**: See [neovide.dev](https://neovide.dev/installation.html)
- **NVM**: `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash`
- **SDKMAN**: `curl -s https://get.sdkman.io | bash`

## Structure

```
~/.dotfiles/
├── bin/          → ~/.local/scripts/
├── neovide/      → ~/.config/neovide/
├── nvim/         → ~/.config/nvim/        (submodule)
├── personal/     → ~/.config/personal/    (submodule, private)
├── sway/         → ~/.config/sway/
├── tmux/         → ~/.tmux.conf
├── waybar/       → ~/.config/waybar/
├── zed/          → ~/.config/zed/
├── zsh/          → ~/.zshrc, ~/.zsh_profile
├── bootstrap     # Setup script
├── install       # Re-link configs
└── uninstall     # Remove symlinks
```

Each directory mirrors the home directory structure. GNU Stow creates symlinks from `$HOME` into this repo.

## Key Bindings

### Sway
- `Alt+Return` — Open terminal (Kitty)
- `Alt+d` — App launcher (Rofi)
- `Alt+hjkl` — Focus navigation
- `Alt+Shift+hjkl` — Move windows
- `Alt+n` — Toggle Waybar
- `Win+Space` — Switch keyboard layout (US/RU/UA)
- `Print` — Screenshot to clipboard
- `Shift+Print` — Area screenshot to clipboard

### Tmux (prefix: Ctrl+A)
- `Ctrl+F` — Fuzzy find project (tmux-sessionizer)
- `prefix+f` — Fuzzy find project (alternative)
- `prefix+hjkl` — Pane navigation
- `prefix+b` — Toggle status bar
- `prefix+D` — Open TODO.md

### Neovim
See [nvim config repo](https://github.com/grok-rs/nvim) for keybindings.

## Managing Configs

```bash
# Re-link all configs after changes
./install

# Link a single package
stow nvim

# Unlink a single package
stow -D nvim

# Remove all symlinks
./uninstall
```
