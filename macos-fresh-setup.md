Setup Macbook from Fresh

# Homebrew

### Install Homebrew & Homebrew apps

- [Homebrew](https://brew.sh/)

### Install software

```bash
brew install arc discord bitwarden bruno raycast 
```

### Dev Environment

If you plan to use my dev environment from my dotfiles, these are required.

```bash
brew install ghostty gh git oh-my-posh neovim tmux lazygit ripgrep yazi fzf fd lsd bash bc coreutils gawk gh glab gsed jq nowplaying-cli
brew install --cask font-monaspace-nerd-font font-noto-sans-symbols-2
```

### Languages & Runtimes
```bash
brew install node oven-sh/bun/bun python go typescript
```

### Language Servers (optional if using neovim)

```bash
brew install typescript-language-server tailwindcss-language-server basedpyright vscode-langservers-extracted
```

### Linters and Formatters

```bash
brew install biome ruff gopls
```

### Optional

```bash
brew install helix visual-studio-code zellij notion starship fastfetch
```

### Fonts (optional)

```bash
brew install --cask font-ubuntu-mono font-jetbrains-mono font-iosevka font-inconsolata font-fira-code font-roboto-mono font-source-code-pro font-azeret-mono font-cascadia-code font-maple font-monaspace font-geist-mono-nerd-font font-anonymous-pro
```

## npm (optional)

```bash
npm i -g emmet-ls @prisma/language-server
```

## Create directories

Note: I use multiple github accounts, so adjust the dirs below as necessary.
If you use my zsh alias' below, there is one `cdp` to quickly access the projects area

```bash
mkdir -p ~/.config ~/.ssh ~/workspaces/github.com/<github-username>/projects ~/workspaces/notes ~/workspaces/courses
```

If you have many mac devices and prefer to store on in iCloud:
```bash
mkdir -p ~/.config ~/.ssh ~/Library/Mobile Documents/com~apple~CloudDocs/workspaces/github.com/<github-username>/projects ~/Library/Mobile Documents/com~apple~CloudDocs/workspaces/notes ~/Library/Mobile Documents/com~apple~CloudDocs/workspaces/courses
```

## SSH

If you don't have an SSH key, generate one following [SSH From Scratch](/ssh-from-scratch.md) and [Multi SSH for different Github Accounts](/multi-github-ssh.md) if needed.
If you have multiple apple devices, I recommend backing these up so you don't have to generate them again.


### From Backup

```bash
open ~/.ssh
```

- Copy files from SSH backup into .ssh directory
- Start the agent

```bash
eval "$(ssh-agent -s)"
```

- Add to key chain

```bash
ssh-add --apple-use-keychain ~/.ssh/id_ed25519_<name>
```

- repeat for each key

## Clone dotfiles

```bash
git clone git@github.com:ionztorm/dotfiles ~/.config
```

## Prep terminal

Open ghostty

### zshrc config

- Create the zshrc configuration file:

```bash
touch ~/.zshrc
```

- Open the file - use vim for now, we will setup neovim later.

```bash
vi ~/zshrc
```

- Add some useful aliases (just copy paste):

To paste in vim, press escape so that you are in Normal mode, then press 'p'

```bash
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

alias tls="tmux ls"
alias tns="tmux new -s"
alias tks="tmux kill-session -t"
alias tka="tmux kill-session -a"
alias tat="tmux attach -t"
```

- Save and exit vim:

To save and exit, press escape so that you are in Normal mode, then type `:wq` and press enter.

Type the folllowing to load the new alias':

```bash
source ~/.zshrc
```

### command line

#### oh my posh

- Add the following line to the end of the zsh config:
    - the theme should work if the dotfiles were downloaded correctly

- Again:

```bash
vi ~/.zshrc
```

- Press 'G' to move to the end of the file, then press 'o' to open a new line. Press 'escape'
to return to normal mode, then press 'p' to paste the below line.

```bash
eval "$(oh-my-posh init zsh --config ~/.config/oh-my-posh/catppuccin_mocka.json)"
```

- Save and exit vim:

Again, to save and exit, press escape so that you are in Normal mode, then type `:wq` and press enter.

Type the folllowing to load the new command line:

```bash
source ~/.zshrc
```

### Multiplexer

#### tmux

- Navigate to a project folder using the terminal

```bash
# for example
cd ~/workspaces/projects/github/my-project # if you chose to store on your mac
cd ~/Library/Mobile Documents/com~apple~CloudDocs/workspaces/projects/github/my-project # if you chose to store on iCloud
```

- Create a tmux session:

```bash
tns <session-name>

# For example: tns my-project
```

- Initiate the tmux theme:

  1) Hold control and press 's'
  2) Realease and press 'I' (capital i)
  if this worked you should get a notification that it's been reloaded, and press escape to continue.
  3) Hold control and press 's'
  4) Release control and press 'r'

  if the theme doesn't load, you may need to kill your session and make a new one.
  1) Hold control and press 's'
  2) Release control and press 'd'
  3) To kill all sessions, type `tmux kill-session -a` in the terminal.
  4) Check there are no sessions with `tls`
  5) If there are no sessions, start a new one with `tns <session-name>`
  6) Hold control and press 's'
  7) Release control and press 'r'
  This should reload the theme.

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

  ```bash
  nv .
  ```

  2) on the 'serve' pane:

  ```bash
  bun --bun run dev
  ```

  3) on the 'explore' pane:

  ```bash
  yazi
  ```

- Disconnect to a session:

  1) Hold control and press 's'
  2) Release control and press 'd'

- View active sessions from terminal:

```bash
tls
```

- Reattach to a session:

```bash
tat <session name>
```

### Neovim

- Open neovim - this will take some time to install plugins and language servers.

```bash
nv .
```

## Optional

### If you chose zellij instead of tmux:

```bash
# in ~/.zshrc

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
```

#### ZelliJ usage

- This is an alternative to tmux - I prefer it.

- install zellij

```bash
brew install zellij
```

- Navigate to a project folder us ing the terminal

```bash
# for example
cd ~/workspaces/projects/github/my-project
```

- Create a zellij session:

```bash
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

```bash
zellij ls
# or
zjls
```

- Reattach

```bash
zellij -a <session name>
# or
zja <session name>
```

### If you chose starship instead of oh-my-posh:


#### Starship

- Install starship

```bash
brew install starship
```

- Add the following line to the end of the zsh config:

```bash
eval "$(starship init zsh)"
```

- Install the starship pure prompt:

```bash
starship preset pure-preset -o ~/.config/starship.toml
```
