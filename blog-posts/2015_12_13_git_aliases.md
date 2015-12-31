### ALIASES

This refers to creating abbreviations/nicks for commands.

##### Advantages

1. Enables us to create simple abbreviations for complex commands that are hard to recall or take a lot of time to type
2. Enable you to *customize* the command names you want to type

git status, git add, git commit, and git checkout are such common commands that it is useful to have abbreviations for them.

There are 2 main ways in which you can add git aliases:

1. Via the **.gitconfig** file [**RECOMMENDED**]

Add the following to the `.gitconfig` file in your `$HOME` directory.

```
[alias]
  co = checkout
  ci = commit
  st = status
  br = branch
  hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
  type = cat-file -t
  dump = cat-file -p
```

2. Shell Aliases (Optional)

This only works if you are running a posix-like shell. Windows users and other non-posix shell users cannot use this method.

If your shell supports aliases or shortcuts, then you can add aliases at that level too.

Add the following to the `.profile` file in your `$HOME` directory.

```
alias gs='git status '
alias ga='git add '
alias gb='git branch '
alias gc='git commit'
alias gd='git diff'
alias go='git checkout '
alias gk='gitk --all&'
alias gx='gitx --all'

alias got='git '
alias get='git '
```

##### Note: Note: Some of these shell aliases are a bit aggressive. In particular, gs will conflict with the Linux GhostScript program. 

#### Use Shell aliases with caution
