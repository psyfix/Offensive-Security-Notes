### Environment Setup

##### Installing Burp Certificate
```
Configure proxy settings on device.
Install the Burp CER root certificate on the device.
Check you can proxy traffic using google search.
Check you can proxy traffic on the app? No? Then there is an SSL pin.
```
##### Objection & Frida.

###### Install Python Packages.
```
pip3 install frida-tools
pip3 install objection
```
###### Download and Execute Frida Server.
```
#Check your frida version.
frida --version

#Check the phones architecture.
adb shell
uname -a 

#Download the correct release that matches the frida version and phone architecture.
https://github.com/frida/frida/releases

#Transfer and execute the Frida Server.
adb push /path/to/frida-server /data/local/tmp/
chmod +x frida-server
./frida-server
```
### Breaking SSL Pin
https://krushnalipane.medium.com/bypassing-android-ssl-pinning-194e41a0d807
###### Objection
```
1. Find the application name first: pm list packages | grep <string>

#Inject directly into the running application.
objection -g nz.innovaapps.valentiawestcoast explore --startup-command "android sslpinning disable"

#Repatch the APK file.
1. objection patchapk --source example.apk
2. install modified apk.
3. objection -g <app_name> explore
4. android sslpinning disable.
```
###### Magisk
```
If you are using a phone that is jail broken using Magisk.
Go to the Magisk settings and turn on Always Trust User Certificates.
```
![[Pasted image 20240327145808.png]]
###### Frida
```
Try the following Frida Script.
_frida -U -f <pkg name/PID> -l fridascript.js
```

###### APK-MITM
```
Install the tool: https://github.com/shroudedcode/apk-mitm
Then run: apk-mitm <your-apk>
Reinstall patched application.
```
![[Pasted image 20240327150043.png]]

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