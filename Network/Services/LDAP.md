
```
#Anonymous search.
#this can be quite finnicky play around with domain and host target ip
ldapsearch -v -x -b 'DC=hutch,DC=offsec' -H 'ldap://<target-ip>' '(objectclass=*)'
```