###### Burp Extensions
```
Magic Byte Selector
Upload Scanner
Autorize
JWT Token
ASP.NET Beautifier
JSLinkFinder
```

###### JWTs
```
#Scanning and Exploitation
https://github.com/ticarpi/jwt_tool.git
jwt_tool.py -t <url> -rc "jwt=xxx" -M pb -np

#Cracking
https://github.com/lmammino/jwt-cracker
hashcat -a 0 -m 16500 jwt.txt passlist.txt

#Reference Attacks
https://auth0.com/blog/critical-vulnerabilities-in-json-web-token-libraries/
```

#### Enumeration
###### JS Finder
```
https://github.com/kacakb/jsfinder
```

Directory Busting
```
feroxbuster -u https://example.com/ -w /usr/share/seclists/Discovery/Web-Content/<word-list>

options
--no-recursion
-b cookie=xxx
```

Fuzzing Parameters
```
ffuf -u "https://example.com/?FUZZ" -c -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt -ac -mc all
```
###### Scanners
```
nikto
nmap
wpscan
joomscan
nuclei
```

##### Spiders
```
ZAP
Burp
Hakrawler
```