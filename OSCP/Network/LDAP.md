
```
#Anonymous search.
ldapsearch -v -x -b 'DC=hutch,DC=offsec' -H 'ldap://192.168.213.122' '(objectclass=*)'
```