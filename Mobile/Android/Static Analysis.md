### Environment Setup

```
MobSF
JADX-GUI
APK Tools
Platform Tools
```
#### Dynamic Analysis
```
Install MobSF and run it on the APK , GG ;)
```
#### Manual Analysis
```
1. Open up the APK file with JADX-GUI. 

Here are some interesting strings to search for:
- key
- http
- https
- AWS
- password
- secret
- username
- firebase.io
- API
- Client
- Server

2.
```

## How to analyse the Manifest file

API Level

- What is the minimum and maximum API level, is it no longer supported by Google?

Exported Activities ([https://aupsham98.medium.com/exploiting-android-activity-activity-android-exported-true-93ffeb263682](https://aupsham98.medium.com/exploiting-android-activity-activity-android-exported-true-93ffeb263682))

- These are activities that can be manually started and executed by third-party applications.
- Sometimes that can reveal sensitive data or another part of the application which could lead to an exploit.

Application Permissions

- These are the permissions the application has on the phone.
- All permissions should be reviewed to ensure they don't create a security risk.
- If the application is writing to external storage, check to see what is being stored there.

BackUp Flag

- Is the BackUp mode set to true?
- This setting defines whether application data can be backed up and restored by a user who has enabled usb debugging. Therefore applications that handle and store sensitive information such as card details, passwords etc. should have this setting set to false to prevent such risks.

Debug Mode

- Is debuggable mode set to true?

### Firebase Enumeration

[https://github.com/Sambal0x/firebaseEnum](https://github.com/Sambal0x/firebaseEnum)

How to view without logging into Google Account

[https://example.firebase.com/.json](https://example.firebase.com/.json)

[https://example.firebase.com/directory/.json](https://example.firebase.com/directory/.json)

![[Pasted image 20240327144713.png]]