### apk 파일 이란?

안드로이드 응용 프로그램 패키지(Android application package)의 약자로, 안드로이드의 소프트웨어와 미들웨어 배포에 사용되는 패키지 파일이다. 



### 방법

**폴더 확인**

android/app/src/main/assets 폴더가 있어야한다. 없으면 만들어야한다.

 

**key 생성**

```
 keytool -genkeypair -v -keystore my-upload-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
```

JSK와 관련된 문구가 뜨지만 무시하고 넘어가도 된다.

생성되는 폴더들을 android/app 폴더로 이동시킨다. keystore 파일은 version control system으로 올라가면 안되므로 커밋시키지 않아야한다.

 

**android/app/build.gradle**

```
android {
    ...
    defaultConfig { ... }
    signingConfigs {
        release { //here
            if (project.hasProperty('MYAPP_RELEASE_STORE_FILE')) {
                storeFile file(MYAPP_RELEASE_STORE_FILE)
                storePassword MYAPP_RELEASE_STORE_PASSWORD
                keyAlias MYAPP_RELEASE_KEY_ALIAS
                keyPassword MYAPP_RELEASE_KEY_PASSWORD
            }
        }
    }
    buildTypes {
        release {
            ...
            signingConfig signingConfigs.release // here
        }
    }
}
```

 

**bundle 파일 생성**

```bash
react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res/
```

 

**release apk 파일 생성**

android/

```
gradlew assembleRelease
```

 

**build apk**

Android Studio > Build > Build Bundle > Build APK

 

**apk 파일 설치**

Build APK가 에러 없이 설치될 경우 app/build/outputs/apk/debug/ 안에 있는 apk 파일을 설치하면 된다.

 

**※ 설치 후 보안상의 이유라는 문구와 함께 설치가 안될 경우**

애플리케이션 > 특별한 접근 > 내 파일 > 이 출처 허용 체크

 

**※ Unable to load script. Make sure you're either running a Metro server**

오류를 찾아본 결과 노드 버전의 문제라서 12.8로 고쳐야 한다고 했으나 내 경우엔 gradlew clean을 실행하고 이 코드를 다시 치니깐 정상적으로 실행됐다.

```bash
react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res/
```

 