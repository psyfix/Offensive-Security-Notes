
```
#Configure your machine to use the squid proxy.

#Attempt to port scan the target machine more for internal ports.
curl --proxy http://<proxy-ip>:3128 http://<target-ip>

#Attempt to port scan the internal network.
curl --proxy http://<proxy-ip>:3128 http://<internal-network>

https://github.com/aancw/spose
```