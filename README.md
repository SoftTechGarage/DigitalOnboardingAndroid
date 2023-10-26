# DigitalOnboardingAndroid SDK
Softtech DigitalOnboarding Android SDK.
## Installation of the Framework
### Android Studio
- Search for `https://github.com/SoftTechGarage/DigitalOnboardingAndroid` in the search bar.
- Set the **Branch** to **release/v0.0.1**. //Please contact Softtech to ask for your version.
- Make sure your project name is selected in **Add to Project**.
- Then, **Add Package**.
## 1: Permissions
```xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.NFC" />
```
## 2: You must add the api key to the plist.
```xml
  <meta-data
    android:name="com.sanalogi.cameralibrary"
    android:value="tokenValue" />
```