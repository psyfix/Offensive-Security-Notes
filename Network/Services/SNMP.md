```
#SNMP Port scan
sudo nmap -sU --open -p 161 <ip> -oA <snmp>

#onesixtyone
onesixtyone -c /usr/share/wordlists/seclists/Discovery/SNMP/common-snmp-community-strings-onesixtyone.txt -i <ip>

#Query for a list of OIDS
snmpwalk -c public -v1 -t 10 <ip>

#Query a specific OID.
snmpwalk -c public -v1 <ip> <oid>

#Query Extended 
snmpwalk -v1 -c public <ip> NET-SNMP-EXTEND-MIB::nsExtendObjects
```
