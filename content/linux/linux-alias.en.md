---
title: My alias
date: 2014-09-29T21:20:27+00:00

---
My favourite alias:

```bash
laptop:/ # cat /home/jose/.bash_alias
# PROMPT
#export PS1="\e[1;33m\u\e[m@\e[1;35m\h\e[m:\e[1;32m\w\e[m\$ \n "

alias ..='cd ..'
alias ...='cd ../..'
alias l='ls -CF'
alias ll='ls -CFlh'
alias la='ls -CFA'
alias lla='ls -CFAlh'
alias lx='ls -X'
alias ld='ls -d'
alias md='mkdir -p'
alias fuck='sudo $(history -p \!\!)'
alias psc='ps xawf -eo pid,user,cgroup,args'
alias grep_jose='grep --color -HinI'</pre>
```