> The instructions are the collective efforts from a few places online. 
Nothing here is my original. But I want to put them together in one place to save people from spending the same time.

First off, bundle.
==================

1. Go to the project directory cd
2. Start the react-native packager if not started
3. Download the bundle to the asset folder:

```sh
$ curl "http://localhost:8081/index.android.bundle?platform=android" -o "android/app/src/main/assets/index.android.bundle"
```
(Thanks : https://github.com/facebook/react-native/issues/2743#issuecomment-140697340)

Note: make sure there is assets folder under android/app/src/main beforehand, and check if there is any error in the packager terminal window after curl.

Secondly, compile release version.
==================================

1. cd to {YOUR_PROJECT}/android
2. Build release version
```sh
$ ./gradlew assembleRelease
```

Thirdly, sign the apk.
======================

1. To generate keystore
```sh
$ keytool -genkey -v -keystore my-keystore.keystore -alias name_alias -keyalg RSA -validity 10000
```
2. To sign an apk
```sh
$ jarsigner -verbose -keystore <path of my-keystore.keystore> <path of apk>  alias_name
```
3. To zip align an apk
```sh
$ zipalign -f -v 4 <your.apk >  <your_aligned.apk>
```
(Thanks : http://stackoverflow.com/questions/26828372/how-to-sign-a-modded-an-apk-on-a-mac-with-apktool)

Lastly, install apk to device.
==============================

1. Connect your phone to computer
2. Install apk 
```sh 
$ adb install {PATH_TO_APK}
```

> Visit http://facebook.github.io/react-native/docs/signed-apk-android.html for more details on generating signed APK

