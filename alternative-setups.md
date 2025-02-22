# Alternative Setups

## Tmux

Use tmux instead of zellij.

Replace the zellij alias in the [Fresh Setup](./macos-fresh-setup.md) with these.

```bash
# in ~/.zshrc

alias tls="tmux ls"                     # list sessions
alias tns="tmux new -s"                 # new session
alias tks="tmux kill-session -t"        # kill named session
alias tka="tmux kill-server"            # kill all sessions
alias tat="tmux attach -t"              # reattach to named session
```

Remember to source the file after adding the aliases.

```bash
source ~/.zshrc
```


## oh-my-posh

Alternative to Oh My Posh.

- Add the following line to the end of the zsh config:

```bash
eval "$(oh-my-posh init zsh --config ~/.config/oh-my-posh/catppuccin_mocka.json)"
```
