# Softtech Digital Onboarding Android SDK
This document walkthroughs the necessary steps that should be taken to integrate the Onboarding Android SDK into your project.

## Prerequisites
- ```NFCReader-[version].aar``` : The NFCReader SDK must be integrated into the project in order to use the Onboarding SDK.
- ```minSdk 24``` : The Onboarding SDK supports android sdk versions starting from 24. The onboarding SDK won't work unless your project root is set to minSDK at least 24.
- ```java compatibility```: Some libraries used in the Onboarding SDK were compiled with Java 17, therefore it is suggested to set your source and target compatibility to Java version-17.
- ```proguard-rules``` : Please add the provided proguard rules in your root project to avoid unexpected behaviours. The instructions for the proguard rules are provided in the following sections.
- ```gradle dependencies```: The dependencies with exact versions from both NFCReader SDK and Onboarding SDK must be included in your app's build gradle. Otherwise, the SDK won't work. The instructions for the gradle dependencies are provided in the following sections.
## Installation of the Framework
### 1. Importing SDKs into your project

- Please make sure that you've downloaded the most recent versions of both Onboarding SDK and NFCReader SDK.
- Place the SDKs under `<root_of_your_project>/libs` or `<root_of_your_project>/app/libs`
- Depending on where you placed your libs folder with respect to the `build.gradle, specify the path of the directory via:

  ```gradle
  repositories {
    flatDir {
      dirs '../libs' // Points to the libs directory
    }
  }
  ```
  Then, add the SDKs to the build.gradle as follows:

  ```gradle
  dependencies {
    implementation(name: 'onboarding-<version>', 'ext': 'aar')
    implementation(name: 'NFCReader-<version>', 'ext': 'aar')
  }
  ```

  Or, without doing so, simply include everything from the libs folder as follows:

  ```gradle
    implementation fileTree(dir: '../libs', include: ['*.jar', '*.aar'])
  ```

### 2. Adding Permissions

Please add the following permission to your `AndroidManifest.xml`

```xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.NFC" />
```

### 3. Setting versions

Please make sure the following java compatibility block is specified under the android block of the build.gradle

```gradle
compileOptions {
    sourceCompatibility JavaVersion.VERSION_17
    targetCompatibility JavaVersion.VERSION_17
}
```

Also, the ```mindSdk```should be set to at least 24.

### 3. Adding Repositories

Please make sure the following repositories are defined, otherwise some libraries might have not found during fetching.

```gradle
maven {
    url 'https://jitpack.io'
}
maven {
    url "https://github.com/jitsi/jitsi-maven-repository/raw/master/releases"
}
```

### 4. Adding Dependencies

```gradle
implementation "com.google.android.material:material:<version>" // version >= 1.7.0

implementation "com.squareup.okhttp3:okhttp:4.9.0"
implementation "com.squareup.okhttp3:logging-interceptor:4.9.0"
implementation "com.squareup.okhttp3:okhttp-urlconnection:4.9.0"
implementation "com.squareup.retrofit2:retrofit:2.9.0"
implementation "com.squareup.retrofit2:converter-gson:2.9.0"

implementation "com.airbnb.android:lottie:3.4.0"
implementation "com.github.bumptech.glide:glide:4.11.0"
annotationProcessor "com.github.bumptech.glide:compiler:4.11.0"

implementation "androidx.camera:camera-camera2:1.2.3"
implementation "androidx.camera:camera-core:1.2.3"
implementation "androidx.camera:camera-lifecycle:1.2.3"
implementation "androidx.camera:camera-view:1.2.3"

implementation 'com.google.mlkit:face-detection:16.1.2'

implementation "pl.droidsonroids.gif:android-gif-drawable:1.2.28"
implementation "cz.adaptech.tesseract4android:tesseract4android:4.7.0"
implementation "edu.ucar:jj2000:5.2"
implementation "org.jmrtd:jmrtd:0.7.42"
implementation "net.sf.scuba:scuba-sc-android:0.0.26"
implementation "net.sf.scuba:scuba-sc-j2se:0.0.21"
implementation "com.github.mhshams:jnbis:2.1.2"

implementation ("org.jitsi.react:jitsi-meet-sdk:8.4.0") { transitive = true }

implementation "com.amplitude:android-sdk:2.34.0" 
```

### 5. Enable databinding

The data binding must be enabled in `build.gradle`.

```gradle
buildFeatures {
    dataBinding true
}
```

### 6. Packaging options

Due to same resources used by different libraries, some files are produced more than once during the build process. Therefore, they should be excluded to be able to have a successful build.
Please add the following block under `android` block of your `build.gradle`.

```gradle
packagingOptions {
    pickFirst 'lib/x86/libc++_shared.so'
    pickFirst 'lib/x86_64/libc++_shared.so'
    pickFirst 'lib/armeabi-v7a/libc++_shared.so'
    pickFirst 'lib/arm64-v8a/libc++_shared.so'
    exclude 'META-INF/versions/9/OSGI-INF/MANIFEST.MF'
}
```

### 7. Proguard Rules

If your application uses `ProGuard`, the following rules should be added, otherwise you might encounter unexpected runtime errors.

```Proguard
-keep class com.softtech.onboarding.conn.model.** { *; }
-keep class org.opencv.** { *;}
-keep class net.sf.scuba.smartcards.IsoDepCardService { *;}
-keep class org.spongycastle.** { *;}
-keep class org.bouncycastle.** { *;}
```
### 8. Miscellaneous

- The Onboarding SDK provides a toolbar. Hence, the theme where the SDK is loaded should have no action bar. Please set the theme to `NoActionBar`.
- During the merging manifests phase of the build, you will receive an error if you have `android:label` attribute defined under the `AndroidManifest.xml`. To resolve this, please add the following attribute:
  ```xml
  tools:replace=“android:label”
  ```

## Initializing the Onboarding SDK

You could use the builder to init the SDK with the required and optional parameters, and start using it. Following is the breakthrough of the publicly accessible functions of the SDK.

- The minimal required parameters to run the SDK

  ```kotlin
  Onboarding
      .setContext(context: Context)
      .setEndpoint(endpoint: String)
      .start()
  ```

- All available options
  ```kotlin
  Onboarding
      .setContext(context: Context) // required
      .setEndpoint(endpoint: String) // required
      .setPredefined(predefined: String) // optional
      .setLanguage(language: String) // optional
      .setProcess(processId: String) // optional
      .setExternalKey(externalKey: String) // optional
      .themeMode(boolean: Boolean) // optional
      .setJson(json: String) // optional
      .start()
  ```

> Breaking through the parameters:

1. `setContext(context: Context)` : The context is needed by the SDK.
2. `setEndpoint(endpoint: String)`: The endpoint for the REST Api must be set.
3. `setPredefined(predefined: String)` : This one is required by the SDK to work properly, but it might not have been set explicitly. This is a unique identifier of your application. If it is not set, the SDK will try to use the package name from the context you have provided via `setContext`
4. `setLanguage(language: String)` : Set to define the language of the SDK. Use language codes such as `tr`,  `en`. If not provided, `tr` will be set by default.
5. `setProcess(processId: String)` : `processId` is a unique identifier and given by the backend when the user starts using the Onboarding. If you already know which process is supposed to be started, such as onboarding a user from a deeplink, you may set this parameter.
6. `setExternalKey(externalKey: String)` : The `externalKey` must be unique for each process. If set, you may track in which step the user at. Otherwise, at each re-init of the SDK for the same device will start the process from scratch. If it is set properly, the users might continue where they have left.
7. `themeMode(theme: Boolean)` : If set to `true`the SDK will run in `Dark Mode`. Likewise, setting `false` will lead to `Light Mode`. Not setting or setting null to this parameter will cause the SDK to determine the theme mode from the default device settings.
8. `setJson(json: String)` : If you want to bypass some steps, you may set some fields via a predefined json string. 

    > Sample JSON for `setJson`
    ```json
    "[{\"code\":\"createLeadParty_tckn\",\"value\":\"Your_TCKN_Here\"},{\"code\":\"createLeadParty_name\",\"value\":\"Your_Name_Here\"},{\"code\":\"createLeadParty_surname\",\"value\":\"Your_LastName\"},{\"code\":\"createLeadParty_phone\",\"value\":\"Your_PhoneNum\"},{\"code\":\"createLeadParty_countryCode\",\"value\":\"+90\"},{\"code\":\"createLeadParty_email\",\"value\":\"Your_EmailAddress\"},{\"code\":\"createLeadParty_primaryContactType\",\"value\":\"PHONE\"},{\"code\":\"createLeadParty_hasNewIdentityCard\",\"value\":\"true\"}]"
    ```

>Example Onboarding SDK Init

```kotlin
Onboarding
    .setContext(requireContext())
    .setEndpoint("https://my.example.end.point.com")
    .setPredefined("com.softtech.example")
    .setLanguage("tr")
    .themeMode(true)
    .start()
```