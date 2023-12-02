#### Manual Inspection
```
#Search every version number and string for public exploits.
#Note interesting functionality and parameters.
1. Wappalyzer.
2. Page Source Code.
3. Application Headers.
4. Application Requests.
5. Browse Application.
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

If you don't find anything:
Brute force directories
Brute force with extensions: php, html, aspx, txt, .git
```
#### FUFF
```
ffuf -u http://192.168.193.25:8082/FUZZ -c -w /usr/share/seclists/Discovery/Web-Content/raft-large-words.txt -ac
```
### Crawling
```
Spider
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

### WebDAV
```
#Used to test WebDav exists
davtest --url <url>

#Used to connect to WebDAv - usually requires credentials
cadaver <ip>
```