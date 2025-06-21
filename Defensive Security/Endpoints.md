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

netstat -anob
- Contains process ID and the name of the process.
- Contains IP address of established connection as well as the port number.
- Established = ongoing remote connection to another system.

TCPView
- GUI + netstat on steroids.
- Microsoft sysinternals tool.
- Can snapshot, can export, can filter by ipv4/6, DNS, etc.


Process Analysis

tasklist
- lists processes.
- tasklist /FI "PID eq <PID/>" - can filter by a specific column value.
- tasklist /FI "PID eq <PID/>" /M - can filter by a specific processes DLLs.

wmic
- Strong for querying information about a specific process id.
- wmic process where processid=<PID/> get name, parentprocessid, processid
- wmic process where processid=<PID/> get commandline

processmonitor

processexplorer
- taskmanager on steroids. sysinternals tool.
- pink = services
- can show DLLs, parent process tree
- can create a memory dump of a process for further analysis.
- can see network connections of proccesses.

Windows Core Processes
System
- PID 4
- Image Path: None
- Parent Process: None

SMSS.exe
- Parent Process: System (4)
- Image Path: SystemRoot/System32/smss.exe