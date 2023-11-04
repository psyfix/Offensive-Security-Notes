```
#ping sweep
fping -a -g <ip_range> 2>/dev/null 

#top1000
nmap -Pn -T4 -F -iL <hosts> -oA top1000

#full+scripts
nmap -Pn -T4 -A -p- -iL <hosts> full
```

#### GOBUSTER
```
#Standard directory bust
gobuster dir -u <url> -w <wordlist> -o <output>

#options
-x <extensions>
--exclude-length <length>

If you don't find anything but do find a directory remember to brute force that directory!!!

```

```
searchsploit
searchsploit -m <module_no>
```