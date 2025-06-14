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
- Base64 Encoding, URL Encoding, HTML Encoding 
- Obscure JavaScript

Abusing Legitimate Sources
- Google Drive, Dropbox etc to host content. - trusted certificate then no flag by detection rules.
- Using trusted reputations to send malware.

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
##### Initial Triage
- Quickly assess and prioritise 
- Who was the email delivered too? (Standard users, Execs, IT, Finance, HR)
##### Header and Sender Examination
- Investigate MTAs, addresses, IPs, etc.
- Identify the true origin and check authenticity. (Reverse DNS, check domain ownership)
##### Content Examination
- Analyse the email content for language, formatting, etc.
- Social engineering red flags.
##### Web and URL Examination
##### Attachment Examination

##### Contextual Examination
- Look for patterns in activity across the organisation.
- Is there a bigger threat going on here?

### Defence Measures
- Take reactive actions
- Take proactive actions
- Communicate with users and stakeholders.

### Documentation and Reporting
- Maintain documentation the whole time this methodology is done.