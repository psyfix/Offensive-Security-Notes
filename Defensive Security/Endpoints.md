Endpoint Security Monitoring
- Process Execution
	- Running proceeses
	- Executable files, PIDs, command-line
	- Parent-child process hierarchy
- File System Changes
	- creation, modification, deletion.
	- File integrity monitoring
- Network Connections
	- Traffic and connections initiated from the endpoint.
	- Associated processes and executables.
- Registry Modifications
	- Monitor registry keys and values

Network Analysis
Check for live connections:
- netstat -anob
- Contains process ID and the name of the process.
- Contains IP address of established connection as well as the port number.
- Established = ongoing remote connection to another system.