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
