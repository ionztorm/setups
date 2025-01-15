# Setup Macbook from Fresh

## Homebrew

### Install Homebrew & Homebrew apps

- [Homebrew](https://brew.sh/)

### Install software

```zsh
brew install arc discord bitwarden bruno raycast 
```

### Dev Environment
```zsh
brew install gh git starship neovim zellij lazygit
```

### CLI Tools
```zsh
brew install ghostty ripgrep yazi fzf fd lsd
```

### Languages & Runtimes
```zsh
brew install node oven-sh/bun/bun python go typescript
```

### Language Servers

```zsh
brew install typescript-language-server tailwindcss-language-server basedpyright vscode-langservers-extracted
```

### Linters and Formatters

```zsh
brew install biome ruff-lsp gopls
```

### Optional

```zsh
brew install helix visual-studio-code tmux notion oh-my-posh fastfetch
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

Note: I use multiple github accounts, so adjust the dirs below as necessary.
If you use my zsh alias' below, there is one `cdp` to quickly access the projects area

```zsh
mkdir -p ~/.config ~/.ssh ~/workspaces/github.com/<github-username>/projects ~/workspaces/notes ~/workspaces/courses
```

## Install Ghostty

- This should already have been installed using the brew command above, but if not:

```zsh
brew install --cask ghostty
```

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


### zshrc config

- Create the zshrc configuration file:

```zsh
touch ~/.zshrc
```

- Add some useful aliases:

```zsh
alias nv="nvim"
alias cl="clear"
alias cdp="cd ~/workspaces/github.com/"
alias nvt="NVIM_APPNAME=testbuild nvim"
alias gs="git status"
alias gc="git commit -m"
alias ga="git add"
alias gaa="git add ."
alias gp="git push"
alias gpf="git push --force"
alias gpl="git pull"
alias gco="git checkout"
alias gcb="git checkout -b"
alias gb="git branch"
alias gl="git log"
alias gd="git diff"
alias gds="git diff --staged"
alias gr="git remote"
alias grr="git remote -v"
alias grrm="git remote remove"
alias grra="git remote add"
alias grru="git remote update"

alias zja="zellij attach"               # attach
alias zjs="zellij -s"                   # new session
alias zjh="zellij -h"                   # help
alias zjl="zellij -l"                   # layout
alias zjn="zellij -n"                   # new session with layout
alias zjls="zellij ls"                  # list sessions
alias zj="zellij"                       # zellij
alias zjd="zellij d"                    # delete session
alias zjda="zellij da"                  # kill session
alias zjk="zellij k"                    # kill session
alias zjka="zellij ka"                  # kill all sessions

alias tls="tmux ls"
alias tns="tmux new -s"
alias tks="tmux kill-session -t"
alias tka="tmux kill-session -a"
alias tat="tmux attach -t"
```

### command line

#### Starship

- Install starship

```zsh
brew install starship
```

- Add the following line to the end of the zsh config:

```zsh
eval "$(starship init zsh)"
```

- Install the starship pure prompt:

```zsh
starship preset pure-preset -o ~/.config/starship.toml
```

#### oh my posh

- Install oh my posh

```zsh
brew install oh-my-posh
```

- Add the following line to the end of the zsh config:
    - the theme should work if the dotfiles were downloaded correctly

```zsh
eval "$(oh-my-posh init zsh --config ~/.config/oh-my-posh/omp.yaml)"
```

### Multiplexer

#### tmux


- Install tmux

```zsh
brew install tmux
```

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

- Navigate to a project folder us ing the terminal

```zsh
# for example
cd ~/workspaces/projects/github/my-project
```

- Create a tmux session:

```zsh
tmux new -s <session-name>

# For example: tmux new -s my-project
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

#### ZelliJ

- This is an alternative to tmux - I prefer it.

- install zellij

```zsh
brew install zellij
```

- Navigate to a project folder us ing the terminal

```zsh
# for example
cd ~/workspaces/projects/github/my-project
```

- Create a zellij session:

```zsh
zellij -s <session-name>
# or, if you used my alias'
zjs <session-name> 

# For example: zjs my-project
```

- zellij panes

    - In Zellij, panes are created by splitting the screen. You can split the screen horizontally or vertically.
    - In place of tmux windows, Zellij uses tabs.

To create these:

Note: if you default to locked mode (recommended!), add CTRL + g before the below bindings.

```
panes: CTRL + p -> n
tabs: CTRL + t -> n
```

To rename:

```
panes: CTRL + p -> c
tabs: CTRL + t -> r
```

- Detach from a session:

```
CTRL + O -> d
```

- List sessions

```zsh
zellij ls
# or
zjls
```

- Reattach

```zsh
zellij -a <session name>
# or
zja <session name>
```

### Neovim

- Open neovim - this will take some time to install plugins and language servers.

```zsh
nvim .
# or, if you used my alias'
nv .
```

