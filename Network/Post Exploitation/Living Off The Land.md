#### Port Scanning
```
#Verify open port
Test-NetConnection -Port 445 192.168.50.151

#Verify range of ports
1..1024 | % {echo ((New-Object Net.Sockets.TcpClient).Connect("192.168.50.151", $_)) "TCP port $_ is open"} 2>$null
```


##### Saving responses in variables.
```
#Example you are curl an internal web server to get code execution.
#Windows

#Use curl.exe instead of curl.
curl.exe -UseBasicParsing http://nickel/?whoami

#Use powershell.
$Resp = Invoke-WebRequest 'http://nickel/?whoami' -UseBasicParsing
	#View the response.
	$Resp.RawContent
```