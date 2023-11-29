# Android build
## build failed
- 설정 체크   
https://reactnative.dev/docs/environment-setup?os=macos&platform=android&guide=native#android-sdk   

- `compileSdkVersion is not specified. Please add it to build.gradle`   
`gradle.properties`에 android.compileSdkVersion=33 명시

- `uses-sdk:minSdkVersion 21 cannot be smaller than version 23 declared in library [:react-native-camera-kit]`   
minSdkVersion = Integer.parseInt(findProperty('android.minSdkVersion') ?: '23'), 21에서 23으로 수정

## kakao build failed
- `Could not find method kotlinOptions() for arguments [build_cuhnpa8pz4l6b0mhsg04etgdl$_run_closure2$_closure9@19a3828a] on extension 'android' of type com.android.build.gradle.internal.dsl.BaseAppModuleExtension.`
