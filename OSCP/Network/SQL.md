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
```