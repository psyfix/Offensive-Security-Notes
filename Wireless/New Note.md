
```
Tools & Hardware:

- A wireless adapter compatible with kali linux or a wifi pineapple from hak5.
- Cracking - hashcat or aircrack
- Wifi tool suites - fluxion or airgeddon
```


```
Scanning and Recon

- Perform a site survey or recon scan of the area to gain information on the target access points.

Handshake Attack

- The primary goal here is to obtain a handshake of the access point you are targeting. It can then be taken offline for cracking.
- While listening for hand shakes from the target attempt a deauth attack. (requires two wifi adapters if no pineapple)
- Take the handshake file offline and attempt to crack it using aircrack or hashcat with a wordlist (attempt to create to a wordlist based on the manufacturer of the router or other social engineering methods).
- If the wifi protocol is weak such as WEP a wordlist is not required and it should be able to be cracked in 5-10 minutes.

Evil Twins

WPS Brute forcing
```