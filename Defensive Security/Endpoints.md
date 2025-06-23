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

csrss.exe
lsass.exe

svchost.exe
- Parent Process: services.exe
- Image Path: SystemRoot/System32/svchost.exe
- Command line always runs with -k parameter.

lsass.exe
- Image Path: SystemRoot/System32/lsass.exe
- Parent Process: wininit.exe
- This is the process that mimikatz dumps the memory from to get credentials.


### 🧩 **Sysmon Event IDs for Process Triage – with Commentary**

| Triage Step                  | Sysmon Event ID(s) | Why It Matters                                                                                                                                                                 |
| ---------------------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **1. Process Creation**      | **1**              | This is your starting point for almost everything. <br>- Full image path<br>- Command-line args <br>- Hashes (MD5, SHA256) <br>- Parent process<br>- User and signature status |
| **2. Network Connections**   | **3**              | Captures outbound TCP connections made by a process. Lets you see potential **C2 traffic**, lateral movement, or data exfiltration. Look for uncommon ports or strange IPs.    |
| **3. File Activity**         | **11**             | Tells you if the process created or modified files. You’ll see paths of dropped payloads or scripts — great for spotting **stage 2 payloads or malware unpacking**.            |
| **4. DLL Loading**           | **7**              | Logs all image (DLL) loads. Good for detecting **unsigned or odd DLLs**, **DLL sideloading**, or **living-off-the-land abuse**.                                                |
| **5. Registry Modification** | **13 / 14**        | Shows changes to the registry. Key for catching **persistence mechanisms** like `Run` keys, services, or `AppInit_DLLs`.                                                       |
| **6. Named Pipe Activity**   | **17 / 18**        | Indicates inter-process communication via named pipes. Useful for detecting **lateral movement tools** like Cobalt Strike or **malware staging frameworks**.                   |
| 7. WMI Activity              | **19 / 20 / 21**   | Logs creation and use of WMI filters, consumers, and bindings. Used in stealthy **persistence**, **recon**, and **remote execution** by adversaries.                           |
### Registry Analysis


##### Cheat Sheets
https://www.sans.org/posters/hunt-evil/


### Persistence
#### Autoruns

##### Registry Modifcation
- Attackers will often modify the registry in windows to create auto runs and execute malicious payloads at login.

| Registry Path                                                      | Scope        | Purpose                    |
| ------------------------------------------------------------------ | ------------ | -------------------------- |
| `HKCU\Software\Microsoft\Windows\CurrentVersion\Run`               | Current user | Programs auto-run at login |
| `HKLM\Software\Microsoft\Windows\CurrentVersion\Run`               | All users    | Programs auto-run at login |
| `HKCU\...\RunOnce` and `HKLM\...\RunOnce`                          | User/All     | One-time auto-run          |
| `HKLM\Software\Microsoft\Windows\CurrentVersion\RunServices`       | System       | Services auto-run (legacy) |
| `HKLM\Software\Microsoft\Windows\CurrentVersion\Winlogon\Userinit` | System       | Userinit programs at logon |
| `HKLM\Software\Microsoft\Windows\CurrentVersion\Winlogon\Shell`    | System       | Shell program at login     |
| `HKLM\SYSTEM\CurrentControlSet\Services`                           | System       | Windows services           |
