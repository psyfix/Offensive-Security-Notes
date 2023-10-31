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
##### Kerberos
```
hashcat -m 13100 -a 0 <hash> <wordlist> --force
```

##### SSH


##### Options
###### Hashcat
-  -r \<rule\>
- --show
- -m \<hash-type\>
- -a \<attack-type\>
- --force

###### John
Need to add options here..................
