### setup git config

`sudo vim ~/.gitconfig`

insert 
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
    ci = commit
    co = checkout
    br = branch
    unstage = reset HEAD --
    last = log -1 HEAD
```


