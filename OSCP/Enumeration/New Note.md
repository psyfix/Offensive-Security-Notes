```
#ping sweep
fping -a -g <ip_range> 2>/dev/null 

#top1000
nmap -Pn -T4 -F -iL <hosts> -oA top1000

#full+scripts
nmap -Pn -T4 -A -p- -iL <hosts> -oA full

#Dont forget UDP.
nmap -sU --open -A -F -T4 -Pn -iL <hosts> -oA udp
```


````
Methodology

1. Check easy ports first. SSH, FTP, SMB.

2. Check HTTP.
	1. Check public exploits.
	2. Resort to manual exploitation LAST.

3. Resort to brute forcing

````

