## 브라우저에 url을 입력하면 무엇이 일어날까?

1. DNS를 통해 IP를 얻는다.
2. IP 주소에 서버와 TCP 3 way handshake를 진행한다.
3. 통신 맺은 서버로 HTTP Request를 보낸다.
4. 서버에서 보낸 HTTP Response를 통해 html 파일을 받는다.
5. 브라우저가 html 파일을 분석해서 화면에 그려준다.



## TCP(Transmission Control Protocol)란?

> 장치들 사이에 논리적인 접속을 성립하기 위해 연결을 설정하여 **신뢰성을 보장하는 연결형 서비스**



### TCP 3way handshake

#### 개념

TCP 통신을 이용하여 데이터를 전송하기 위해 장치 간 <u>**연결을 설정**</u>하는 과정



#### 과정

1. Client에서 Server로 SYN 패킷 전송
2. Server에서 Client로 SYN 패킷과 ACK 응답 전송
3. Client에서 Server로 ACK 응답 전송

![tcp-3way-handshake](images/tcp-3way-handshake.png)



### TCP 4way handshake

#### 개념

TCP의 <u>**연결을 해제**</u>하는 과정



#### 과정

1. Client에서 Server로 연결을 종료하겠다는 FIN flag 전송
2. Server는 Client로 ACK 응답을 보내고, 자신의 통신이 끝날때까지 **CLOSE_WAIT**상태로 기다림
3. Server가 통신이 끝났으면 Client로 FIN flag 전송
4. Client는 Server로 ACK 응답 보냄

![tcp-4way-handshake](images/tcp-4way-handshake.png)





#### 참고

> - https://mindnet.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-22%ED%8E%B8-TCP-3-WayHandshake-4-WayHandshake
> - https://gmlwjd9405.github.io/2018/09/19/tcp-connection.html