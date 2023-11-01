#### SharpHound
```
powershell -ep bypass
Import-Module .\sharphound.ps1
Copy powershell script to host and import module
Invoke-BloodHound -CollectionMethod All -OutputDirectory C:\Users\<user>\Desktop\ -OutputPrefix "audit results"
```



- Invoke-BloodHound -CollectionMethod All -OutputDirectory C:\Users\<user>\Desktop\ -OutputPrefix "audit results"

Copy data over to kali.

- Host share in kali and then copy see file transfer commands.

## BloodHound

sudo neo4j start

sudo bloodhound

[http://localhost:7474](http://localhost:7474)

neo4j:kali

- Import zipped data.
- Check Shortest Paths Analysis.
- Right click objects that are owned. For example users and client machines.
- Then choose "Shortest Path to Domain Admins from owned Principals".