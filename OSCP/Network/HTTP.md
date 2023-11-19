#### Manual Inspection
```
1. Search any string indicating a technology and its version number.
2. Inspect headers, use wappalyzer, inspect page source code.
```
#### GOBUSTER
```
#Standard directory bust
gobuster dir -u <url> -w <wordlist> -o <output>

#options
#Specify Extensions
-x <extensions>

#Exclude Length
--exclude-length <length>

#Exlcude Status Code
-b <status_code>

If you don't find anything but do find a directory remember to brute force that directory!!! Gobuster is not recursive.
```
#### FUFF
```

```
### Crawling
```
Spider
```

### Passive
```
Wappalyzer
Page Source Code
```

### Scanning
```
wpscan
joomscan
droopescan
nikto
nmap 
```

### Git
```
git-dumper <url> <output_dir>
git status
git reset --hard
git log
git diff <commit_id>
```