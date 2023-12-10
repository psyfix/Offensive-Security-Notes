##### LM
```
john --format=lm <hash> <wordlist>
hashcat -m 3000 -a 0 <hash> <wordlist> --force
```
##### NTLM
```
john --format=nt <hash> <wordlist>
hashcat -m 1000 -a 0 <hash> <wordlist> --force
```
##### NTLMv1
```
john --format=netntlm <hash> <wordlist>
hashcat -m 5500 -a 0 <hash> <wordlist> --force
```
##### NTLMv2
```
john --format=netntlmv2 <hash> <wordlist>
hashcat -m 5600 -a 0 <hash> <wordlist> --force
```
##### AS-REP 
```
hashcat -m 18200 -a 0 <hash> <wordlist> --force
```
##### KERB
```
hashcat -m 13100 -a 0 <hash> <wordlist> --force
```

##### SSH
```
ssh2john id_rsa > ssh.hash
john --wordlist=/usr/share/wordlists/rockyou.txt ssh.hash
```

##### KEEPASS
```
#Don't forget to remove the "Database:" from the hash afterwards.
keepass2john Database.kdbx > keepass.hash

hashcat -m 13400 -a 0 <hash> <wordlist> --force
```
##### ZIP
```
#To determine whether it is a valid zip file or just malformed data use.
file <file-name>

#FCrack
fcrackzip -u -v -D -p ~/Desktop/rockyou.txt <zip_file>

#Regular ZIP
	zip2john

#7ZIP
	#Extract zip
	7z e <zip>
	#Extract hash
	7z2john

hashcat can auto detect the hash.
```

##### PDF
```
pdfcrack
```

##### Mozilla / Firefox
```
#Run this inside the directorty containing the key3 / key4 / login.json files.
python firepwd.py
Python3 - https://github.com/lclevy/firepwd
```