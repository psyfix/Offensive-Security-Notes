#### Phishing Attack Types

```
Information Gathering
- Collecting data through reconnaissance
- Verifying existing accounts, craft credible phishes.
- Collected data is often used in follow up attacks.
- Tracking pixel 
	- 1x1 image not visible. 
	- When image is loaded by the client tells the attackers server.
	- collects information via http request: ip, location, device type, email client type, operating system.
- Can paste information from HTTP request into https://explore.whatismybrowser.com/useragents/parse/ then you get clear info on email client and browser etc.

Credential Harvesting
- Obtain credentials from victims.
- Relay entered passwords and MFA codes 

Malware Delivery
- Malicious attachments or links (to download).
- Drive by downloads - visiting a website automatically downloads malware.

Phishing Email Ideas
Microsoft Related
- Onedrive new file shared.
- User signed in as you from another location.


```

Attack Techniques
```
Email & Domain Spoofing
- Homograph Attack (https://www.irongeek.com/homoglyph-attack-generator.php)
- Generates similiar looking domains. (https://dnstwist.it/)

URL Manipulation
- URL Shortening Subdomain Spoofing.
- Subdomain Spoofing. (https://dnstwist.it/)
- Homograph Attacks. (https://www.irongeek.com/homoglyph-attack-generator.php)
- Typosquatting.

QR Code Generation
- https://www.qrcode-generator.de/

Encoding
- Encoding content within emails that still renders in the HTML.
- Base64 Encoding, URL Encoding, HTML Entity Encoding 
- Obscure JavaScript

Abusing Legitimate Sources
- Google Drive, Dropbox etc to host content. - trusted certificate then no flag by detection rules.
- Using trusted reputations to send malware.

Bypassing SPF, DMARC, DKIM
- Register a look a like domain with your own SPF record.

```

### Phishing Attack Methodology
Reconnaissance 
```
Passive
Gather information on target.
Active
- Send a test email to verify the recipient exists and email is delivered.
- Use a tracking pixel to gather information about the target.
```

Execution
```
Develop a phishing email.
- Use attack techniques such as domain and email spoofing, encoding and abusing legitimate sources.

```

Exfiltration
```

```

### Phishing Analysis Methodology
##### Automated Analysis
- [https://www.phishtool.com/](https://www.phishtool.com/)
##### Initial Triage & Containment
- Quickly assess and prioritise 
- Who was the email delivered too? (Standard users, Execs, IT, Finance, HR)
- Determine Scope
- Check logs (M365, GCP etc.)
- Quarantine all related emails.
- Block sender artifacts - block senders, malicious domains, ip addresses.
- Change Credentials & Reset Sessions.
- Restore and reset affected systems.
##### Header and Sender Examination
###### Identify the origin IP address (Reverse DNS, check domain ownership)
- Examine the email source.
- https://mha.azurewebsites.net/ - This will format the source and headers nicely to read. (Can be downloaded and run locally)
```
Reply-To: This header is often different to the from address because often an attacker does not have control over the from address as its spoofed.

Return-Path: This is where the bounceback mail should go too.

Message-ID: This ID is given by the first MTA that handles the message. Often an indicator of the original attackers domain it was sent from.

X-Sender-IP: The IP address of the device or server the mail came from.
X-Originating-IP: The IP address of the device or server the mail came from.

Received: A received chain that is useful for tracking the route the message took before being delivered. In reversed chronological order. The first header is the closest to the recipient.

DKIM-Signature: Contains the signed signature from the domain that was verified.
```

Reverse the IP address.
- Document information about the sender.
- whois
- iplookup

Verify the Domain or IP Address.
- Is it malicious or unknown?

Verify the authentication checks.
- Analyse the authentication-check header. Did it pass a SPF and DKIM check?

##### Content Examination
- Analyse the email content for language, formatting, etc.
- Social engineering red flags.
##### Web and URL Examination
- Analyse email to see type of encoding if any.
- Use Cyber Chef to decode
- Use cyber chef to extract urls and then also defang them.
- Bonus: https://github.com/MalwareCube/Email-IOC-Extractor this tool extracts important data and auto defangs it for emails.
- Verify and investigate URLs: 
	- Virustotal - checks blacklist
	- URL2PNG - shows photo of the url like eyewitness.
	- urlscan.io
	- urlvoid
	- wannabrowser - grabs the actual response of the url/page
##### Attachment Examination
- Static Analysis
	- Get the file hash and compare to databases: Virustotal
- OLE File Analysis
	- Use a tool such as OLE dump to dump the contents of macro embedded files and search for malicious indicators. (https://github.com/DidierStevens/DidierStevensSuite/blob/master/oledump.py)
		- oledump.py <file/>
		- oledump.py <file/> -s <source/>
		- oledump.py <file/> -s <source/> -S
		- oledump.py <file/> -s <source/> --vbadecompresscorrupt
- PDF File Analysis (https://github.com/DidierStevens/DidierStevensSuite/blob/master/pdf-parser.py)
	- 
- Perform malware analysis in a sandbox environment.
	- There is free tools such as HYBRID ANALYSIS. https://www.hybrid-analysis.com/


##### Contextual Examination
- Look for patterns in activity across the organisation.
- Is there a bigger threat going on here?

### Phishing Defence Measures
##### Reactive Defence
- Change Credentials & Reset Sessions.
- Restore and reset affected systems.
- Quarantine all related emails.
- Create mail flow rules to block.
	-  Block sender artifacts - block senders, malicious domains, ip addresses.
	-  Block web related artifacts.
##### Proactive Defence
###### Email Filtering
- Email security applications that filter on the email gateway level.
	- Custom rulesets and mail flow rules.
	- Deploy additional blacklists.
	- Scan attachments and links in real time.
	- Block recently registered domains.
	- File extension blocks / allowlist.
- Mark External emails with a warning.
###### Email Authentication
- Configure SPF
- Configure DKIM & DMARC.
###### Security Awareness
- Regular awareness videos.
- Monthly phishing simulations.
### Documentation and Reporting
```
Phishing Analysis Report Template 

Headers 
====================================== 
Date: 
Subject: 

To: From: 

Reply-To: 
Return-Path: 

Sender IP: 
Resolve Host: 

Message-ID: 

URLs 
======================================= 



Attachments 
====================================== 

Attachment Name: 
MD5: 
SHA1: 
SHA256: 


Description 
====================================== 



Artifact Analysis 
====================================== 
Sender Analysis: 



URL Analysis: 



Attachment Analysis: 



Verdict 
====================================== 




Defense Actions 
======================================



```

### Resources
- Phishing Pot - collection of real emails to practice on.
- PhishTank 
- Malware Bazaar. - search for PDFS then can do PDF extraction and inspection.