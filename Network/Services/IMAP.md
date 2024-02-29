
```
Reference: https://book.hacktricks.xyz/network-services-pentesting/pentesting-imap

#Login
nc <ip> 143
	tag login <user>@localhost <password>
	tag LIST "" "*"
	tag SELECT INBOX
	tag fetch <message-no> BODY[HEADER] BODY[1]
```