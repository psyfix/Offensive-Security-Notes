```
#ping sweep
fping -a -g <ip_range> 2>/dev/null 

#top1000
nmap -Pn -T4 -F -iL <hosts> -oA top1000

#full+scripts
nmap -Pn -T4 -A -p- -iL <hosts> full
```



```
searchsploit
searchsploit -m <module_no>
```