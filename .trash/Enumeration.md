```
#ping sweep
fping -a -g <ip_range> 2>/dev/null 

#top1000
nmap -Pn -T4 -F -iL <hosts> -oA top1000

#full+scripts
nmap -Pn -T4 -sV -sC -p- <ip> -oN full --open

#Dont forget UDP.
nmap -sU --open -A -F -T4 -Pn <ip> -oN udp

#Check vulns
nmap -Pn -T4 -p --script "vuln" <hosts> -oA vulns
```


````
Methodology

1. Check easy ports first. SSH, FTP, SMB.

2. Check HTTP.
	1. Check public exploits.
	2. Resort to manual exploitation LAST.

3. Resort to brute forcing

````

