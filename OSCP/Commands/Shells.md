#### Shells

#### Upgrades

```
#interactive upgrade
python3 -c 'import pty; pty.spawn("/bin/bash")'

#interactive upgrade
python3 -c 'import pty; pty.spawn(["env","TERM=xterm-256color","/bin/bash","--rcfile", "/etc/bash.bashrc","-i"])'

#enables clear
export TERM=xterm
```