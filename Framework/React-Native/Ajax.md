### Ajax(Asynchronous Javascript And Xml)

JavaScript를 사용한 비동기 통신이며, 클라이언트와 서버간의 XML 데이터를 주고받는 기술이다.
XMLHttpRequest객체를 이용해서 전체 페이지를 리로드하지 않고 필요한 데이터만 로드할 수 있다.



**Axios vs Fetch**

|        |                            axios                             |                            fetch                             |
| ------ | :----------------------------------------------------------: | :----------------------------------------------------------: |
| 장점   | - 거의 모든 브라우저에서 지원<br />- 응답 시간 초과 설정 가능<br />- JSON 데이터 자동변환 가능<br />- node.js에서 사용<br />- request aborting(요청 취소) 가능<br />- 요청을 하던 중간에 실패할 경우, .then을 실행하지않고 catch가 실행 | - JavaScript의 내장 라이브러리이므로 import 없이 사용 가능<br />- 라이브러리 업데이트에 따른 오류 발생 방지(react native는 업데이트가 잦아서 라이브러리가 쫓아오는 경우가 많음, fetch를 쓰면 이를 방지)<br />- response timeout API를 제공하지 않아 네트워크 오류가 발생할 경우 계속 기다림 |
| 단점   |               많은 기능을 지원하는 만큼 무거움               |                   일부 브라우저에선 지원 x                   |
| 공통점 |                    return: Promise Object                    |                                                              |



### fetch

```javascript
// Example POST method implementation:

postData('http://example.com/answer', {answer: 42})
  .then(data => console.log(JSON.stringify(data))) // JSON-string from `response.json()` call
  .catch(error => console.error(error));

function postData(url = '', data = {}) {
  // Default options are marked with *
    return fetch(url, {
        method: 'POST', // *GET, POST, PUT, DELETE, etc.
        mode: 'cors', // no-cors, cors, *same-origin
        cache: 'no-cache', // *default, no-cache, reload, force-cache, only-if-cached
        credentials: 'same-origin', // include, *same-origin, omit
        headers: {
            'Content-Type': 'application/json',
            // 'Content-Type': 'application/x-www-form-urlencoded',
        },
        redirect: 'follow', // manual, *follow, error
        referrer: 'no-referrer', // no-referrer, *client
        body: JSON.stringify(data), // body data type must match "Content-Type" header
    })
    .then(response => response.json()); // parses JSON response into native JavaScript objects 
```

- body: JSON.stringify(),

  - 서버에 body를 보내줄 때, json 형태로 보내줘야 함

- .then(response => response.json())

  - 서버로부터 응답 받으면 우선 json형태로 변환해야 함

- headers:  {

  ​	'Content-Type': 'application/json',

     },

  - 서버에 보낼 body가 json 형태이므로 헤더에 json 형태라는 것을 알려줘야함



### ALLOWED_HOST

- 허용되는 IP를 지정해줌

- DEBUG가 True일 땐,  `'localhost'`, `'127.0.0.1'`,`'[::1]'`가 자동으로 들어감
- amulator는 localhost가 아니므로 `'10.0.2.2'`나 `'*'`을 넣어줘야함
  - `'*'`은 보안상의 이슈로 인해 쓰지 않을 것을 권장함



### 참고

> [velog.io/@leeeeunz/TIL-35.-axios%EC%99%80-fetch%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90](https://velog.io/@leeeeunz/TIL-35.-axios와-fetch의-차이점)