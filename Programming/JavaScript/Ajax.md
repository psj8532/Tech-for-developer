# Ajax

> Asynchronous JavaScript And XML

##### 정의

Ajax는 XMLHttpRequest 객체를 사용하여 서버와 통신하는 것으로, <u>JavaScript를 사용한 비동기 통신, 클라이언트와 서버간에 XML 데이터를 주고받는 기술</u>입니다. 



##### 특징

- 비동기성

  전체 페이지를 새로고침 하지 않고, 서버에 요청하여 필요한 부분만 업데이트 할 수 있습니다.



## Callback

##### 콜백 함수(Callback Function)란?

Ajax를 이용한 비동기 요청을 보낼 때, 함수를 같이 전달하여 요청이 완료되면 이 함수를 실행합니다. 이 함수를 **콜백 함수**라고 부릅니다. 이러한 콜백 함수를 사용함으로써 비동기 요청이 완료되면 자동으로 함수가 실행되기 때문에 편리합니다.



##### 콜백 지옥(Callback Hell)

콜백 함수를 중첩적으로 사용하다보면 <u>코드가 복잡해지고 가독성이 떨어집니다</u>. 또한, 요청 중간에 오류가 발생한다면 <u>디버깅과 유지보수가 어렵습니다</u>. 그래서 콜백 함수를 중첩하여 사용하는 것은 권장되지 않습니다. 이 문제를 해결하기 위한 방안으로 `promise`와 `async/await`가 있습니다.

```javascript
class UserStorage {
    login(username, password, onSuccess, onError) {
        setTimeout(() => {
            if (
                (username === 'test1' && password === 'asdf') ||
                (username === 'test2' && password === 'asdf')
            ) {
                onSuccess(username);
            } else {
                onError(new Error('not found'));
            }
        }, 1000);
    }

    getData(username, onSuccess, onError) {
        setTimeout(() => {
            if (username === 'test1') {
                onSuccess({ name: 'test1', role: 'admin' });
            } else {
                onError(new Error('no access'));
            }
        }, 1000);
    }
}

const userStorage = new UserStorage();
const id = prompt('enter your username');
const password =  prompt('enter your password');
userStorage.loginUser(
    id,
    password, 
    username => {
        userStorage.getRoles(
            username,
            userData => {
                alert(`username: ${userData.name}, role: ${userData.role} role`);
            },
            error => {
                console.log(error);
            },
        );
    },
    error => console.log(error)
);
```



## Promise

##### promise란?

`promise` 객체는 **비동기 요청의 미래 결과 값(성공, 실패)**을 나타내는 것으로, 비동기 요청이 완료되는 시점에 결과 값을 알려주겠다고 약속하는 것입니다. 또한, promise는 `ES6`에 추가 된 객체입니다.



##### 상태

- 대기(pending): 이행하거나 거부되지 않은 초기 상태
- 이행(fulfilled): 연산이 성공적으로 완료
- 거부(rejected): 연산이 실패



##### 결과 값

- 성공
  - `Promise.resolve()` 메서드를 통해 Promise 객체를 반환 
  - `.then()`에서 사용
- 실패
  - `Promise.reject()` 메서드를 통해 Promise 객체를 반환
  - .catch()에서 사용



##### 예제

```javascript
class UserStorage {
    login(username, password) {
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                if (
                    (username === 'test1' && password === 'asdf') ||
                    (username === 'test2' && password === 'asdf')
                ) {
                    resolve(username);
                } else {
                    reject(new Error('not found'));
                }
            }, 1000);
        })
    }

    getData(username) {
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                if (username === 'test1') {
                    resolve({ name: 'test1', role: 'admin' });
                } else {
                    reject(new Error('no access'));
                }
            }, 1000);
        })
    }
}

const userStorage = new UserStorage();
const username = prompt('enter your username');
const password =  prompt('enter your password');
userStorage.login(username,password)
    .then(userStorage.getData) // .then(username => userStorage.getData(username))
    .catch(error => console.error(error))
```



## async + await

promise를 이용하면 콜백 지옥에서 탈출할 수 있습니다. 하지만 이러한 promise도 많아지면 코드의 가독성이 떨어집니다. async와 await을 이용하여 해결할 수  있습니다.



##### async

함수 앞에 async를 붙여주면 promise를 사용한 것과 같이 비동기 요청을 보낼 수 있습니다.

```javascript
async function getData() {
    setTimeout(()=> {
        return 'train';
    }, 1000)
}

const data = getData();
data.then(console.log);
console.log(data);
// Promise...
// train
```



##### await

```javascript
function delay(time) {
    return new Promise(resolve => setTimeout(resolve, time))
}

async function getNum() {
    await delay(1000);
    return '10';
}

async function getChar() {
    await delay(1000);
    return 'a';
}

// function pickData() {
//     return getNum()
//         .then(num => {
//             return getChar()
//                 .then(ch => `${num} + ${ch}`);
//         });
// }

async function pickData() {
    const numPromise = getNum();
    const charPromise = getChar();
    const num = await numPromise;
    const ch = await charPromise;
    return `${num} + ${ch}`;
}

pickData().then(console.log); // 10 + a
```



##### 유용한 APIs

```javascript
function pickAllData() {
    return Promise.all([getNum(), getChar()])
        .then(data => data.join(' + '));
}
pickAllData().then(console.log);

function pickOnlyOne() {
    return Promise.race([getNum(), getChar()]);
}
pickOnlyOne().then(console.log); // 작업이 먼저 끝난 것만 보여줌
```



# Refference

> - https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise
> - https://www.youtube.com/watch?v=s1vpVCrT8f4&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=11