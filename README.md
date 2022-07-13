### setup git config

`curl -L https://raw.github.com/git/git/master/contrib/completion/git-prompt.sh > ~/.bash_git`

`sudo vim ~/.gitconfig`

```
# This is Git's per-user configuration file.
[user]
# Please adapt and uncomment the following lines:
#       name = Casper Rasmussen
#       email = cr@nodes.dk
[push]
        default = matching
[alias]
    st = status
    co = checkout
    nb = checkout
    df = diff
    ci = commit
    cv = commit
    br = branch
    ca = commit
    cp = cherry-pick
    nb = checkout
    cv = commit
    ca = commit
[color]
    branch = auto
    diff = auto
    status = auto
```

### setup bashrc
`touch .bashrc`

`sudo vim .bashrc`

```
source ~/.bash_git

# ~/.bashrc: executed by bash(1) for non-login shells.
# see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)
# for examples

# If not running interactively, don't do anything
case $- in
    *i*) ;;
      *) return;;
esac

# don't put duplicate lines or lines starting with space in the history.
# See bash(1) for more options
HISTCONTROL=ignoreboth

# append to the history file, don't overwrite it
shopt -s histappend

# for setting history length see HISTSIZE and HISTFILESIZE in bash(1)
HISTSIZE=1000
HISTFILESIZE=2000

# check the window size after each command and, if necessary,
# update the values of LINES and COLUMNS.
shopt -s checkwinsize

# If set, the pattern "**" used in a pathname expansion context will
# match all files and zero or more directories and subdirectories.
#shopt -s globstar

# make less more friendly for non-text input files, see lesspipe(1)
[ -x /usr/bin/lesspipe ] && eval "$(SHELL=/bin/sh lesspipe)"

# set variable identifying the chroot you work in (used in the prompt below)
if [ -z "${debian_chroot:-}" ] && [ -r /etc/debian_chroot ]; then
    debian_chroot=$(cat /etc/debian_chroot)
fi

# set a fancy prompt (non-color, unless we know we "want" color)
case "$TERM" in
    xterm-color|*-256color) color_prompt=yes;;
esac

# uncomment for a colored prompt, if the terminal has the capability; turned
# off by default to not distract the user: the focus in a terminal window
# should be on the output of commands, not on the prompt
#force_color_prompt=yes

if [ -n "$force_color_prompt" ]; then
    if [ -x /usr/bin/tput ] && tput setaf 1 >&/dev/null; then
    # We have color support; assume it's compliant with Ecma-48
    # (ISO/IEC-6429). (Lack of such support is extremely rare, and such
    # a case would tend to support setf rather than setaf.)
    color_prompt=yes
    else
    color_prompt=
    fi
fi

if [ "$color_prompt" = yes ]; then
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
else
    PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi
unset color_prompt force_color_prompt

# If this is an xterm set the title to user@host:dir
case "$TERM" in
xterm*|rxvt*)
    PS1="\[\e]0;${debian_chroot:+($debian_chroot)}\u@\h: \w\a\]$PS1"
    ;;
*)
    ;;
esac

# enable color support of ls and also add handy aliases
if [ -x /usr/bin/dircolors ]; then
    test -r ~/.dircolors && eval "$(dircolors -b ~/.dircolors)" || eval "$(dircolors -b)"
    alias ls='ls --color=auto'
    #alias dir='dir --color=auto'
    #alias vdir='vdir --color=auto'

    alias grep='grep --color=auto'
    alias fgrep='fgrep --color=auto'
    alias egrep='egrep --color=auto'
fi

# colored GCC warnings and errors
#export GCC_COLORS='error=01;31:warning=01;35:note=01;36:caret=01;32:locus=01:quote=01'

# some more ls aliases
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'

# Add an "alert" alias for long running commands.  Use like so:
#   sleep 10; alert
alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'

# Alias definitions.
# You may want to put all your additions into a separate file like
# ~/.bash_aliases, instead of adding them here directly.
# See /usr/share/doc/bash-doc/examples in the bash-doc package.

if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi

# enable programmable completion features (you don't need to enable
# this, if it's already enabled in /etc/bash.bashrc and /etc/profile
# sources /etc/bash.bashrc).
if ! shopt -oq posix; then
  if [ -f /usr/share/bash-completion/bash_completion ]; then
    . /usr/share/bash-completion/bash_completion
  elif [ -f /etc/bash_completion ]; then
    . /etc/bash_completion
  fi
fi
```


### setup bash_profile
`touch .bash_profile`

`sudo vim .bash_profile`

```
BASH_INTERACTIVE=true
BASH_LOGIN=false
HISTCONTROL=ignoredups
export HISTCONTROL

# Load special node bash settings
if [ -f ~/.profile ];
then
        . ~/.profile
fi

if [ -f ~/.git-flow-completion ];
then
        . ~/.git-flow-completion
fi

if [ -f ~/.aliases ];
then
    . ~/.aliases
fi

if [ -f ~/.custom_alias ];
then
    . ~/.custom_alias
fi

# Load users own settings
if [ -f ~/.bash_local ];
then
        . ~/.bash_local
fi

# vim as default editor
export EDITOR=vim

# ls aliasses
alias l="ls -l"
alias ll="ls -la"

# navigation aliases
alias ..="cd ../"
alias ...="cd ../../"

# aliases changing default behaviors
alias grep="grep --color=auto"
alias mkdir="mkdir -p"
alias less="less -r"
alias tree="tree -C"

# convenience aliases
alias scls="screen -ls"
alias syntax="find . -name '*.php' -exec php -l {} \;" # php syntax check in current folder (+subs)
alias grin='grep -rin'
alias now='date +"%T"'

export GIT_PS1_SHOWDIRTYSTATE="yes"
export GIT_PS1_SHOWSTASHSTATE="yes"
export GIT_PS1_SHOWUNTRACKEDFILES="yes"
export GIT_PS1_SHOWUPSTREAM="auto"

```

### Update keyboard repeats
```bash
defaults write -g InitialKeyRepeat -int 10 # normal minimum is 15 (225 ms)
defaults write -g KeyRepeat -int 1 # normal minimum is 2 (30 ms)
```

### Colors terminal

```
brew install starship
```

### Git
```
git config --global push.default current
```
