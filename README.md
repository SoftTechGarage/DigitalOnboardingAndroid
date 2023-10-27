# DigitalOnboardingAndroid SDK
Softtech DigitalOnboarding Android SDK.
## Installation of the Framework
### Android Studio
- Set the **Branch** to recent vers.
- Make sure your project name is selected in **Add to Project**.
- Then, **Add Package**.
## 1: Permissions
```xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.NFC" />
```
## 2: You must add the api key to the Android Manifest.
```xml
  <meta-data
    android:name="com.sanalogi.cameralibrary"
    android:value="tokenValue" />
```
