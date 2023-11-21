
```
#Anonymous search.
ldapsearch -v -x -b 'DC=hutch,DC=offsec' -H 'ldap://<target-ip>' '(objectclass=*)'
```