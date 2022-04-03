# audio_session_issue52

Sample code to reproduce `module 'audio_session' not found` bug

https://github.com/ryanheise/audio_session/issues/52

## Getting Started

The `main` branch demonstrates the build error:

<details>

<summary>flutter build ios --no-codesign</summary>

```
Running "flutter pub get" in audio_session_issue52...              616ms
Warning: Building for device with codesigning disabled. You will have to
manually codesign before deploying to device.
Building com.daohoangson.audioSessionIssue52 for device (ios-release)...
Running pod install...                                           1,945ms
Running Xcode build...                                                  
 └─Compiling, linking and signing...                        844ms
Xcode build done.                                           30.6s
Failed to build iOS app
Error output from Xcode build:
↳
    ** BUILD FAILED **


Xcode's output:
↳
    Writing result bundle at path:
    	/var/folders/17/pp2qvl7n1rd60k_xpt6jn84r0000gn/T/flutter_tools.6Q0PUd/flutt
    	er_ios_build_temp_dir1eVzkx/temporary_xcresult_bundle

    /xxx/audio_session_issue52/ios/Runner/GeneratedPluginRegistrant.m:12:9: fatal error: module 'audio_session' not found
    @import audio_session;
     ~~~~~~~^~~~~~~~~~~~~
    1 error generated.
    note: Using new build system
    note: Planning
    note: Build preparation complete
    note: Building targets in dependency order

    Result bundle written to path:
    	/var/folders/17/pp2qvl7n1rd60k_xpt6jn84r0000gn/T/flutter_tools.6Q0PUd/flutt
    	er_ios_build_temp_dir1eVzkx/temporary_xcresult_bundle


Parse Issue (Xcode): Module 'audio_session' not found
/xxx/audio_session_issue52/ios/Runner/GeneratedPluginRegistrant.m:11:8


Encountered error while building for device.
```

</details>

<details>

<summary>flutter doctor -v</summary>

```
[✓] Flutter (Channel stable, 2.10.3, on macOS 11.3 20E232 darwin-x64, locale en)
    • Flutter version 2.10.3 at /xxx
    • Upstream repository https://github.com/flutter/flutter.git
    • Framework revision 7e9793dee1 (4 weeks ago), 2022-03-02 11:23:12 -0600
    • Engine revision bd539267b4
    • Dart version 2.16.1
    • DevTools version 2.9.2

[✓] Android toolchain - develop for Android devices (Android SDK version
    33.0.0-rc2)
    • Android SDK at /xxx
    • Platform android-31, build-tools 33.0.0-rc2
    • ANDROID_HOME = /xxx
    • Java binary at: /Applications/Android Studio.app/Contents/jre/Contents/Home/bin/java
    • Java version OpenJDK Runtime Environment (build 11.0.10+0-b96-7281165)
    • All Android licenses accepted.

[✓] Xcode - develop for iOS and macOS (Xcode 13.2.1)
    • Xcode at /Applications/Xcode.app/Contents/Developer
    • CocoaPods version 1.11.2

[✓] Chrome - develop for the web
    • Chrome at /Applications/Google Chrome.app/Contents/MacOS/Google Chrome

[✓] Android Studio (version 2020.3)
    • Android Studio at /Applications/Android Studio.app/Contents
    • Flutter plugin can be installed from:
      🔨 https://plugins.jetbrains.com/plugin/9212-flutter
    • Dart plugin can be installed from:
      🔨 https://plugins.jetbrains.com/plugin/6351-dart
    • Java version OpenJDK Runtime Environment (build 11.0.10+0-b96-7281165)

[✓] VS Code (version 1.66.0)
    • VS Code at /Applications/Visual Studio Code.app/Contents
    • Flutter extension version 3.36.0

[✓] Connected device (2 available)
    • macOS (desktop) • macos  • darwin-x64     • macOS 11.3 20E232 darwin-x64
    • Chrome (web)    • chrome • web-javascript • Google Chrome 100.0.4896.60

[✓] HTTP Host Availability
    • All required HTTP hosts are available

• No issues found!
```

</details>

## Workaround

Bumping the `IPHONEOS_DEPLOYMENT_TARGET` to 11.0 fixes the build.
See branch [workaround](https://github.com/daohoangson/flutter-audio_session-issue52/tree/workaround)
(commit [f35d2c00](https://github.com/daohoangson/flutter-audio_session-issue52/commit/f35d2c001ceaafc8579065167fe1a44deb36ad0a)).
