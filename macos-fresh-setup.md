# Install Homebrew & Homebrew apps

- [Homebrew](https://brew.sh/)

## Languages and Language Servers

```zsh
brew install node typescript python go vscode-langservers-extracted typescript-language-server gopls tailwindcss-language-server
```

```zsh
npm i -g emmet-ls @prisma/language-server
```

## Software

```zsh
brew install gh helix starship arc neovim tmux bruno biome oven-sh/bun/bun
```

```zsh
brew install --cask github discord visual-studio-code cursor bitwarden
```

## Fonts

```zsh
brew install --cask font-ubuntu-mono font-jetbrains-mono font-iosevka font-inconsolata font-fira-code font-roboto-mono font-source-code-pro font-azeret-mono font-cascadia-code font-maple font-monaspace font-geist-mono-nerd-font font-anonymous-pro
```

# Restore Configs

## Create config directory

```zsh
mkdir ~/.config
```

## Install Ghostty

- [Ghostty terminal](https://github.com/mitchellh/ghostty)

## Clone dotfiles

```zsh
cd ~/.config
git clone git@github.com:ionztorm/dotfiles
```

# SSH Setup for Multi-github accounts

## Generate Key

```zsh
ssh-keygen -t ed25519 -C "email"

# set file name
/Users/leonlonsdale/.ssh/id_ed25519_<domain>_username

# set passphrase and confirm
```

## Add to SSH Agent

```zsh
# start the agent
eval "$(ssh-agent -s)"
# returns an agent pid

# write config in vim - github example
vi ~/.ssh/config
# add
HostName github-<username>
    Host github.com
    User git
    AddKeysToAgent yes
    UseKeychain yes
    IdentityFile ~/.ssh/id_ed25519_github_<username>

# write file
:w <enter>

# add key to agent - omit apple keychain if not on mac / did not set passcode.
ssh-add --apple-use-keychain ~/.ssh/id_ed25519_<domain>_<username>

# enter passphrase

# copy public key
pbcopy < ~/.ssh/id_ed25519_<domain>_<username>.pub
```

## Add key to Github

1. Goto Github.com
2. click profile image
3. go to settings
4. choose SSH and GPG keys
5. click New SSH key
6. give it a name in title and
7. paste the key in key.

## Using the correct SSH on github push/fetch for your repo

```zsh
# Navigate to the project directory and set local project config
git config user.name "<github username>"
git config user.email "<github email>"

# Check they saved
git config user.name
git config user.email

# Add remote origin

git remote add origin git@<ssh-hostname>:<username>/<repo>.git

# or update existing

git remote set-url origin git@<ssh-hostname>:<username>/<repo>.git
```
