Setup Macbook from Fresh

# Homebrew

### Install Homebrew & Homebrew apps

- [Homebrew](https://brew.sh/)

Pay attention to this install. It will ask for your password during the process, and after it has finished,
you will need to run some commands to finalise the installaion and add it to your path. It will tell 
you what to do at the end of the install.

```bash

### Dev Environment

If you plan to use my dev environment from my dotfiles, these are required.

```bash
brew install ghostty gh git oh-my-posh neovim tmux lazygit ripgrep yazi fzf fd lsd zoxide regex
```

### Install software

This is stuff I like to use. Adjust as necessary.

```bash
brew install zed-browser discord bitwarden bruno raycast notion obsidian
```

### Languages & Runtimes
```bash
brew install node oven-sh/bun/bun python go typescript
```

### Language Servers (optional if using neovim, install if you choose helix)

```bash
brew install typescript-language-server tailwindcss-language-server basedpyright vscode-langservers-extracted
```
```bash
npm i -g emmet-ls @prisma/language-server
```

### Linters and Formatters

```bash
brew install biome ruff gopls
```

### Optional

```bash
brew install helix visual-studio-code zellij notion starship fastfetch
```

### Popular Coding Fonts (optional)

```bash
brew install --cask font-ubuntu-mono font-jetbrains-mono font-iosevka font-inconsolata font-fira-code font-roboto-mono font-source-code-pro font-azeret-mono font-cascadia-code font-maple font-monaspace font-geist-mono-nerd-font font-anonymous-pro
```
## Create directories

Note: I use multiple github accounts, so adjust the dirs below as necessary.

```bash
mkdir -p ~/.config ~/.ssh ~/Library/Mobile Documents/com~apple~CloudDocs/workspaces/github.com/<github-username>/projects ~/Library/Mobile Documents/com~apple~CloudDocs/workspaces/notes ~/Library/Mobile Documents/com~apple~CloudDocs/workspaces/courses
```

## SSH

1. If you don't have an SSH key, generate one following [SSH From Scratch](/ssh-from-scratch.md)
2. If you have multiple GitHub accounts, take a look at [Multi SSH for different Github Accounts](/multi-github-ssh.md) if needed.
3. If you have multiple apple devices, I recommend backing these up so you don't have to generate them again.

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
# SSH
git clone git@github.com:ionztorm/dotfiles ~/.config

# HTTPS
git clone https://github.com/ionztorm/dotfiles.git ~/.config
```

Or, if you only want the neovim config:

```bash
# SSH
git clone git@github.com:ionztorm/sennvim.git ~/.config

# HTTPS
git clone https://github.com/ionztorm/sennvim.git ~/.config
```

## Prep terminal

Open ghostty

### setup neovim and zshrc config

- Create the zshrc configuration file:

```bash
nvim ~/.zshrc
```

- Add some useful aliases (just copy paste):
- Setup oh-my-posh
- Setup zoxide

To paste in vim, press escape so that you are in Normal mode, then press 'p'

```bash
alias cl="clear"
alias ls="lsd"
alias lsa="ls -a"
alias lsl="ls -l"
alias lsla="ls -la"
alias lst="ls --tree"

# neovim

alias nv="nvim"

# git

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

#tmux

alias tls="tmux ls"                     # list sessions
alias tns="tmux new -s"                 # new session
alias tks="tmux kill-session -t"        # kill named session
alias tka="tmux kill-server"            # kill all sessions
alias tat="tmux attach -t"              # reattach to named session

# python
alias pvenv="python3 -m venv .venv"
alias pvact="source .venv/bin/activate"

eval "$(oh-my-posh init zsh --config ~/.config/oh-my-posh/catppuccin_mocka.json)"
eval "$(zoxide init zsh)"
export PATH=$PATH:$HOME/go/bin
```

- Save and exit vim:

To save and exit, press escape so that you are in Normal mode, then type `:wq` and press enter.

Type the folllowing to load the new alias':

```bash
source ~/.zshrc
```

In some cases, you may need to restart the terminal. Try running `z ~/.config`. If you get an error, restart the terminal.

### Multiplexer

#### tmux

- Navigate to a project folder using the terminal

```bash
# for example
z ~/Library/Mobile Documents/com~apple~CloudDocs/workspaces/projects/github/my-project
```

- Create a tmux session:

```bash
tns <session-name>

# For example: tns my-project
```

Next:

1) Hold `control` and press `s` then press `I`
2) Hold `control` and press `s` then press `r`

This should load the tmux config and install plugins.

If it did not, you may need to restart.

3. Detach from a session: Hold `control` and press `s` then press `d`
4. Type `tks` to kill all sessions.
5. Recreate your session with `tns <session-name>`
6. Repeat steps 1 and 2.

You can create new windows with `control` + `s` then `c` and switch between them with `control` + `s` then `n` or `p` (or their index number).

You can rename the window with `control` + `s` then `,`

Or you can close a window with `control` + `s` then `x`

To detach from a session, press `control` + `s` then `d`
To reattach to a session, use `tat <session-name>` in the terminal.

To see a list of sessions, use `tls` in the terminal.


## Alternatives

You can alternativley use:

- Zellij instead of tmux
- starship instead of oh-my-posh
- helix instead of neovim

You can adjust this setup guide by following the apply the changes in the [Alternative Setups](./alternative-setups.md) guide.

Note that Helix does not require any setup.
