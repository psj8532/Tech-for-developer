### Network Error

**문제**

axios로 요청을 보내면 Error Network Error 메시지가 뜬다. 이 문제는 다양한 원인으로 인해 발생하게 되는데 여러 방법을 시도해본 결과 내 문제는 react native의 문제였다.

**해결방법**

1. https 사용

   - ios는 보안상의 이유로 https를 사용해야 한다.

   - android는 https를 사용하지 않아 http로 써야 한다. 하지만, 기본적으로 http는 사용할 수 없기 때문에 다음과 같은 설정으로 http를 허용해야 한다.

     - ${}>android>app>src>debug>AndroidManifest.xml

     - application 태그 내에 다음과 같이 true로 설정

       - android:usesCleartextTraffic="true"

         ※ 내 컴퓨터의 경우 default로 설정되어 있었다.

 2. 내 컴퓨터의 IP 주소 사용

    localhost 대신에 실제 IP 주소를 사용했으나 요청 자체가 안 보내졌다. 또한, IP 주소를 직접 넣을 경우 보안 상의 이슈가 발생할 수 있어 다른 방법을 찾아보았다.

3. fetch 사용

   axios와 같이 비동기 요청을 보내는 함수이다. axios에 기능이 더 많아 보통 axios를 쓰지만, react native에선 다양한 문제들로 인해 fetch를 많이 사용한다고 한다. 따라서, axios를 fetch로 모두 바꿨다. 하지만 이 방법으로도 역시 해결이 되지 않았다.

   ※ Network request failed라고 뜬다.

4. localhost 변경

   react native는 앱을 구현하는 것이기 때문에 애뮬레이터가 필요하다. 하지만 애뮬레이터는 컴퓨터 안에 또 다른 가상 디바이스에서 켜진 것이기 때문에 주소에 localhost로 쓰면 접근할 수 없다. 따라서, localhost 대신 `애뮬레이터의 IP주소`를 넣어야 한다.

   ∴ localhost(127.0.0.1):port => `10.0.2.2:port`

   ※ 이 방법으로 문제를 해결했다.





### FormData

**문제**

AJAX 요청을 보낼 때, Body에 FormData 객체를 넣어서 보내면 Network error가 발생

**해결 방법**

1. FormData 객체 안에 type 지정

   FormData 안에 type: "image/jpeg"를 넣어주었다. Ios에선 'image/jpg'로 Android에선 'image/jpeg'를 넣어주어야 한다. FromData를 console로 찍어 본 결과 type이 없었기 때문에 이것이 문제였다고 생각하였다. 하지만, type과 name을 지정해줘도 여전히 network error가 발생했다.

2. Flipper 버전 변경

   > in android/gradle.propertie

   - change from FLIPPER_VERSION=`0.37`.0 to FLIPPER_VERSION=`0.52.1`

   Flipper의 버전이 현재 0.37.0인데 이를 0.46.0이나 0.52.1으로 바꿔보는 것을 추천하였다. 하지만 flipper의 버전만 바꾸면 react native 버전과의 호환 문제로 애뮬레이터가 켜지지 않았다.

3. Interceptor 제거

   >  in android/app/src/debug/java/com/{yourProject}/ReactNativeFlipper.java // // //comment in line 43 

   - builder.addNetworkInterceptor(new FlipperOkhttpInterceptor(networkFlipperPlugin)); // 주석처리

   이 방법을 적용해 본 결과, FormData로 AJAX 요청을 보내도 정상적으로 서버에 도달했다.

