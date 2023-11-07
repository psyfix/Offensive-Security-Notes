#### SharpHound
```
powershell -ep bypass
Import-Module .\sharphound.ps1
Invoke-BloodHound -CollectionMethod All -OutputDirectory C:\Users\<user>\Desktop\ -OutputPrefix "audit results"
```
#### BloodHound

```
sudo neo4j start
sudo bloodhound
http://localhost:7474 (neo4j:kali)
```
- Import zipped data.
- Check Shortest Paths Analysis.
- Right click objects that are owned. For example users and client machines.
- Then choose "Shortest Path to Domain Admins from owned Principals".