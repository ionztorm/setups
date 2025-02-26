# Alternative Setups

## Tmux

Use zellij instead of tmux.

Replace the tmux alias' in the [Fresh Setup](./macos-fresh-setup.md) with these.

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

Remember to source the file after adding the aliases.

```bash
source ~/.zshrc
```

## starship

Alternative to Oh My Posh.

- Add the following line to the end of the zsh config:

```bash
eval "$(starship init zsh)"
```
