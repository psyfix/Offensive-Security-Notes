
```
#SNMP Port scan
sudo nmap -sU --open -p 161 <ip> -oA <snmp>

#onesixtyone
onesixtyone -c community -i <ip>

#Query for a list of OIDS
snmpwalk -c public -v1 -t 10 <ip>

#Query a specific OID.
snmpwalk -c public -v1 <ip> <oid>
```
