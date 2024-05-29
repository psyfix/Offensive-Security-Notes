###### Burp Extensions
```
Magic Byte Selector
Upload Scanner
Autorize
JWT Token
ASP.NET Beautifier
JSLinkFinder
GAP Burp Extension
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

GAP Burp Extension
1. Get paramters
2. SQL Fuzz: ffuf -w param.txt:PARAM -w ~/PayloadsAllTheThings/SQL\ Injection/Intruder/Generic_Fuzz.txt:VAL -u https://example.com?PARAM=VAL -c -mc 400,500
3. XSS Fuzz: ffuf -w param.txt:PARAM -w xss.txt:VAL -u https://example.com?PARAM=VAL -c -mr "VAL" -c
4. PT / LFI Fuzz:

Don't forget to try POST as well on the param fuzzing.
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
echo "https://www.planit.com/" | ./hakrawler -u
```