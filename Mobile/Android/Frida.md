### Installation

##### Client
```
pip3 install frida-tools
frida --version
```

#### Server
```
adb shell
uname -a 
Download correct release that matches architecture: https://github.com/frida/frida/releases
adb push /path/to/frida-server /data/local/tmp/
chmod +x frida-server
./frida-server
```

### Bypassing Emulator and Root Detection
#### Analysis
Understand what part of the code is doing the detection. 
		1. Use a decompiler such as JADX-GUI to view the code.
		2. Search for strings such as "Root" "Detection" "Emulator" "Jail"
		3. Then decide what method to use to bypass.

#### Bypasses
##### Frida
```
1. Download latest copy of Frida Server and run on the android device. (https://github.com/frida/frida/releases)
2. From PowerShell run the bypass script. (https://codeshare.frida.re/@KishorBal/multiple-root-detection-bypass/)
	a. frida --codeshare KishorBal/multiple-root-detection-bypass -f nz.innovaapps.valentiawestcoast -U
```
##### Magisk
```
1. Root a device using Magisk.
2. Use the inbuilt root bypass on Magisk.
```

