# Setup Macbook from Fresh

## Homebrew

### Install Homebrew & Homebrew apps

- [Homebrew](https://brew.sh/)

### Install software

```zsh
brew install gh git starship arc neovim tmux discord bitwarden ripgrep lazygit node bruno biome oven-sh/bun/bun yazi typescript python go vscode-langservers-extracted typescript-language-server gopls tailwindcss-language-server
```

### Optional

```zsh
brew install helix visual-studio-code
```

### Fonts

```zsh
brew install --cask font-ubuntu-mono font-jetbrains-mono font-iosevka font-inconsolata font-fira-code font-roboto-mono font-source-code-pro font-azeret-mono font-cascadia-code font-maple font-monaspace font-geist-mono-nerd-font font-anonymous-pro
```

## npm

```zsh
npm i -g emmet-ls @prisma/language-server
```

## Create directories

```zsh
mkdir -p ~/.config ~/.ssh ~/Desktop/code/projects ~/Desktop/code/notes ~/Desktop/code/courses
```

## Install Ghostty

- [Ghostty terminal](https://github.com/mitchellh/ghostty)

## SSH

### From Backup

```zsh
open ~/.ssh
```

- Copy files from SSH backup into .ssh directory
- Start the agent

```zsh
eval "$(ssh-agent -s)"
```

- Add to key chain

```zsh
ssh-add --apple-use-keychain ~/.ssh/id_ed25519_<name>
```

- repeat for each key

## Clone dotfiles

```zsh
git clone git@github.com:ionztorm/dotfiles ~/.config
```

## Prep terminal

### tmux

- Install the tmux plugin manager:

```zsh
git clone https://github.com/tmux-plugins/tpm ~/.config/tmux/plugins/tpm
```

- Install the tmux catpuuccin theme:

[Catppuccin TMUX Theme](https://github.com/catppuccin/tmux)

```zsh
mkdir -p ~/.config/tmux/plugins/catppuccin
git clone -b v2.1.2 https://github.com/catppuccin/tmux.git ~/.config/tmux/plugins/catppuccin/tmux
```

### starship

- Create the zshrc configuration file:

```zsh
touch ~/.zshrc
```

- Add the following line to the end of the zsh config:

```zsh
eval "$(starship init zsh)"
```

- Install the starship pure prompt:

```zsh
starship preset pure-preset -o ~/.config/starship.toml
```

### tmux and neovim Setup

- Navigate to a project folder us ing the terminal

```zsh
# for example
cd Desktop/code/projects/my-project
```

- Create a tmux session:

```zsh
tmux new -s <session-name>

# For example: tmux new -s my-project
```

- Open neovim - this will take some time to install plugins and language servers.

```zsh
nvim .
```

- Initiate the tmux theme:

  1) Hold control and press 's'
  2) Release control and press 'r'

- Create some new tmux panes:

  1) Hold control and press 's'
  2) Release control and press 'c'

Repeat this step for as many panes as you want. I like to have 4 in total, 1 for neovim, one for dev server, one for package installs, and one for file tree.

- Navigate between panes:

  1) Hold control and press 's'
  2) Release control and press 0 / 1 / 2 / 3 (zero indexed)

- Rename panes:

  1) Hold control and press 's'
  2) Release control and press ','
  3) Enter a name.

Names I use are: code / serve / bun or node / explore

- Set up panes:

  1) on the 'code' pane:

  ```zsh
  nvim .
  ```

  2) on the 'serve' pane:

  ```zsh
  bun --bun run dev
  ```

  3) on the 'explore' pane:

  ```zsh
  yazi
  ```

- Disconnect to a session:

  1) Hold control and press 's'
  2) Release control and press 'd'

- View active sessions from terminal:

```zsh
tmux ls
```

- Reattach to a session:

```zsh
tmux attach -t <session name>
```
