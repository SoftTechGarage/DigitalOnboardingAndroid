# Softtech Digital Onboarding Release 2.6.0 and NFCReader release 0.2.14
This document walkthroughs the necessary steps that should be taken to integrate the latest SDKs into your project.

## Updated dependencies

The following libraries should be used with the minimum of the given versions.

- `androidx.appcompat:appcompat:1.7.1` (for edge to edge support required by targetsdk 35)
- `org.jitsi.react:jitsi-meet-sdk:10.3.0'` { transitive = true } (for android 14 crash)
- `com.google.mlkit:face-detection:16.1.7` (for 16kb support)
- `androidx.camera:camera-camera2:1.4.2` (for 16kb support)
- `androidx.camera:camera-core:1.4.2` (for 16kb support)
- `androidx.camera:camera-lifecycle:1.4.2` (for 16kb support)
- `androidx.camera:camera-view:1.4.2` (for 16kb support)
- `pl.droidsonroids.gif:android-gif-drawable:1.2.29` (for 16kb support)
- `cz.adaptech.tesseract4android:tesseract4android:4.9.0` (for 16kb support)

## Target SDK

> The target sdk must be minimum of 35.

## NOTES

> To be able to support 16kb page sizes and targeting the minimum sdk of 35, the AGP and Gradle versions were bumped as well, if any build errors happen, we suggest you to compile your project with at least the following versios:

- Android Gradle Plugin (AGP): 8.5.1
- Gradle: 8.7

## FULL CHANGELOG

- `targetSdkVersion` from 34 to 35
- `AGP` version from 8.3.2 to 8.5.1 
- `Gradle` version from 8.4 to 8.7
- `androidx.appcompat:appcompat` version from 1.5.1 to 1.7.1
- `org.jitsi.react:jitsi-meet-sdk` version from 8.4.0 to 10.3.0
- `com.google.mlkit:face-detection` version from 16.1.2 to 16.1.7
- `androidx.camera:camera-camera2` version from 1.2.3 to 1.4.2
- `androidx.camera:camera-core` version from 1.2.3 to 1.4.2
- `androidx.camera:camera-lifecycle` version from 1.2.3 to 1.4.2
- `androidx.camera:camera-view` version from 1.2.3 to 1.4.2
- `pl.droidsonroids.gif:android-gif-drawable` version from 1.2.28 to 1.2.29
- `cz.adaptech.tesseract4android:tesseract4android` version from 4.7.0 to 4.9.0
- removed deprecated `statusBarColor`
- supported `edge to edge` functionality
- Retry functionality added for face recognition process.
- Trade icon added on confirmation page.
- Fixed keyboard preventing the scroll.
- Fixed button disabled on required field selection.
- Removed unused font `OCRAStd.otf`
- Updated `ndk version` from 23.1.7779620 to 26.1.10909125
- Recompiled native libraries with 16kb memory page size support.