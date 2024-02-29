
```
ARP Scanning - useful when firewalls are aggressively blocking traffic.
1. netdiscover -i tap0 -r 10.10.10.0/24

Ping Sweep
1. 1..255 | % {"10.10.3.$($_): $(Test-Connection -count 1 -comp 10.10.3.$($_) -quiet)"}
2. 
```