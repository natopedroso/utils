# APP .aab TO .apk TO INSTALL VIA ADB

- You will need java istalled
- ## Get the bundletool (https://github.com/google/bundletool/releases)
- make a directory for it
- rename it to bundletool.jar
- to convert to apk command:

```
java -jar bundletool.jar build-apks --bundle=app.aab --output=app.apks --mode=universal --ks=app.jks --ks-key-alias=App
```

--ks and --ks-key-alias needed if you will put the certificate

- after it rename the app.apks to app.zip
- extract it
- rename universal.apk to the app.apk
- now you can install via adb

```
adb install app.apk
```

hope it helped you!
