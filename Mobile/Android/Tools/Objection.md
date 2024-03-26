
### SSL Pinning
```
1. Find the application name first: pm list packages | grep <string>

#Inject directly into the running application.
1. objection -g nz.innovaapps.valentiawestcoast explore --startup-command "android sslpinning disable"

#Repatch the APK file.
1. objection patchapk --source example.apk
```