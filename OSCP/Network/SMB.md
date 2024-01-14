#### No Creds
```
enum4linux -a <ip>
enum4linux -a -u "guest" -p " " <ip>
for host in $(cat hosts.txt); do <command> "$host"; done

smbmap -u "" -p "" -P 445 -H <ip>
smbmap -u "guest" -p "" -P 445 -H <ip>

crackmapexec smb <ip> -u "" -p ""
crackmapexec smb <ip> -u "guest" -p ""

#Scan for CVES such as eternalblue
nmap -T4 -p445 --script smb-vuln* <ip>
```

#### Got Creds

```
impacket-smbclient '<domain>/<user>:<password>@<ip>'

crackmapexec smb <target_ips> -u <user_list> -p <pass_list> -d <domain> --continue-on-success --shares
```