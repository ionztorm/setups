Setup Macbook from Fresh

# Homebrew

### Install Homebrew & Homebrew apps

- [Homebrew](https://brew.sh/)

Homebrew is a package manager for MacOS and Linux. It's what I use to keep my packages up to date. You can likely use whichever package manager you prefer, but you'll have to double check that the packages exist.

To install homebrew, visit the link above and follow the installation instructions.

### Installing Packages

The following commands will install the packages I use. Feel free to add or remove items

#### Dev Environment

##### Terminal and Editor

```bash
brew install ghostty helix tmux
```

##### Command Line Tools and Utilities

```bash
brew install gh git lazygit ripgrep fzf lsd yazi zoxide regex
```

##### Languages

```bash
brew install typescript go python
```

##### Runtimes

```bash
brew install node oven-sh/bun/bun
```

##### Language Tools (LSP, Formatters, Linters)

```bash
brew install gopls ruff typescript-language-server tailwindcss-language-server basedpyright vscode-langservers-extracted biome prettier
```

```bash
npm i -g emmet-ls @prisma/language-server
```

##### Software

```bash
brew install discord bitwarden bruno raycast obsidian
```

### Optional

```bash
brew install visual-studio-code neovim zellij starship
```

### Markdown live preview (Helix users only - this is covered in nvim)

If you are using my neovim config, live preview of html / md files cah be acheieved using the keymap: `<leader>ls`. This is not possible in Helix yet, so we can use a github cli extension:

Install (requires github cli which wrs installed above):

```bash
gh extension install yusukebe/gh-markdown-preview
```

Now we can run the command:

```bash
gh markdown-preview <file name>
```

This loads the markdown file in your browser with github formatting. It uses a live server so updates on save.

## Create directories

Note: I use multiple github accounts, so adjust the dirs below as necessary.

```bash
mkdir -p ~/.config ~/.ssh
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

### zshrc config

- Create the zshrc configuration file:

```bash
hx ~/.zshrc
```

Let's:

- Add some useful aliases for lsd and git (just copy paste):
- Setup oh-my-posh
- Setup zoxide

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

# tmux

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
export PATH=$PATH:$HOME/go/bin         # Sometimes homebrew doesn't add this to the path
```

- Save and exit. Helix works the same way as vim/neovim - press `esc` to enter normal mode and type `:wq`.

Source the file to load the changes.

```bash
source ~/.zshrc
```

In some cases, you may need to restart the terminal. Try running `z ~/.config`. If you get an error, restart the terminal. `z` is the command used in place of `cd` when using zoxide.

### Tmux

Tmux is a `T`erminal `Mu`ltiple`x`er - basically it allows you to create sessions that you can attach to and detach from, but the sessions remain active (as long as the device remains turned on). You can create a session for a particular development project, with servers running, detatch from it and re-attach at a later date to find the server still running and your code editor still active.

- Navigate to a project folder using the terminal

```bash
# for example
z project/directory
```

- Create a session:

```bash
tns <session-name> # often the project name

# For example: tns my-project
```

Quick keybind reference:

- `ctrl` + `s` -> `c` = create new window
- `ctrl` + `s` -> `,` = rename window
- `ctrl` + `s` -> `x` = close window
- `ctrl` + `s` -> `num` = where num is an index number - to switch between windows.
- `ctrl` + `s` -> `r` = reload config

## Alternatives

You can alternativley use:

- zellij instead of tmux
- starship instead of oh-my-posh
- neovim instead of helix

You can adjust this setup guide by following the apply the changes in the [Alternative Setups](./alternative-setups.md) guide.

Note that Helix does not require any setup.
