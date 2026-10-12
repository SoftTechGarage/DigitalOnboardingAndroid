# Softtech Digital Onboarding Android SDK
This document walkthroughs the necessary steps that should be taken to integrate the Onboarding Android SDK into your project. Both ```onboarding-2.9.0.aar``` and ```NFCReader-0.2.15.aar ``` must be used by the main app to apply the changes.

## CHANGELOG (Onboarding v2.9.0 & NFCReader 0.2.15)
- targetSdk version bumped from 35 to 36 for both OnboardingSDK and NFCReaderSDK.
- Build gradle tool version bumped from 8.5.1 to 8.6.0 (With new jitsi version, minimum 8.6.0 is required, lower versions might lead to build errors)
- The updated version of the jitsi must be added in the build.gradle dependencies as follows: 
<br>```implementation ("org.jitsi.react:jitsi-meet-sdk:13.2.0") { transitive = true }```