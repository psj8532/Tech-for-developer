### Splash Screen이란?

앱을 실행했을 때, 연결이 완료 되기전에 나타나는 화면이다. 로딩화면이라고 보면 된다.



### 사용 방법

1. 라이브러리 설치

   ```bash
   yarn add react-native-splash-android
   yarn add -D @bam.tech/react-native-make # Splash image 설정 모듈 설치
   ```

2. 이미지 만들기

   splash screen 용은 최소 3000x3000(px) 이어야한다.

   https://pixlr.com/x/

3. 이미지 저장할 폴더 생성

   android/app/src/res/images에 이미지 복사

   반드시 위 경로일 필요는 없음

4. splash image 생성

   ```
   react-native set-splash --path ./android/app/src/res/images/splash.png --resize contain --background "#FFFFFF"
   ```

   --resize option의 경우 default는 center이지만 이미지가 잘리지 않기 위해서는 contain으로 설정



4번 과정까지 끝내면 MainActivity.java 등을 건드릴 필요없이 자동으로 세팅된다.

※내 경우 파일 만들기 및 세팅을 직접하고 4번을 진행하다보니 SplashScreen화면에서 더이상 작동하지 않는 등의 오류가 발생하였다. 따라서, 세팅을 따로 하지말고 4번을 진행해야 오류없이 작동한다.

