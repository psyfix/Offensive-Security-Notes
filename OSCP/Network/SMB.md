#### No Creds
```
enum4linux -a -u " " -p " " <ip>
enum4linux -a -u "guest" -p " " <ip>

smbmap -u "" -p "" -P 445 -H <ip>
smbmap -u "guest" -p "" -P 445 -H <ip>

crackmapexec smb <ip> -u "" -p ""
crackmapexec smb <ip> -u "guest" -p ""
```

#### Got Creds

```
impacket-smbclient '<domain>/<user>:<password>@<ip>'

crackmapexec smb <target_ips> -u <user_list> -p <pass_list> -d <domain> --continue-on-success --shares
```