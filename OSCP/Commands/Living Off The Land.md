Verify open port:

Test-NetConnection -Port 445 192.168.50.151

Verify range of ports:

1..1024 | % {echo ((New-Object Net.Sockets.TcpClient).Connect("192.168.50.151", $_)) "TCP port $_ is open"} 2>$null