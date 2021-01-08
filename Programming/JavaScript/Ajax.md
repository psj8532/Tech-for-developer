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



##### 콜백 지옥이 생기는 이유

**처리 결과를 외부로 반환하거나 상위 스코프의 변수에 할당할 수 없습니다.** 비동기 함수를 호출하면 함수 내부의 비동기로 동작하는 코드가 완료되지 않았더라도 기다리지 않고 즉시 종료됩니다. 즉, 비동기 함수 내부의 비동기로 동작하는 코드는 비동기 함수가 종료된 이후에 완료되기 때문에 외부로 반환하거나 상위 스코프의 변수에 할당하면 기대한 대로 동작하지 않습니다.

따라서, 비동기 함수의 처리 결과에 대한 후속 처리를 위해서는 비동기 함수 내부에서 수행해야합니다. 이때, 후속 처리 수행을 콜백 함수로 전달하게 됩니다. 이러한 작업이 여러번 중첩된다면, 코드의 가독성도 떨어지고 유지보수도 힘들어집니다. 이 때문에, **콜백 지옥**이 생겨난 것입니다.



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



##### 정적 메서드

- resolve, reject

  resolve와 reject 각각 개별적으로 사용하는 방법입니다. resolve는 인수로 전달받은 값을 resolve하는 프로미스를 생성하고, reject는 reject하는 프로미스를 생성합니다.

  ```javascript
  const resolvedPromise = Promise.resolve([1, 2, 3]);
  resolvedPromise.then(console.log); // [1, 2, 3]
  // 위 코드는 아래와 동일
  const resolvedPromise = new Promise(resolve => resolve([1, 2, 3]));
  ```

  ```javascript
  const rejectedPromise = Promise.reject(new Error('Error!'));
  rejectedPromise.catch(console.log); // Error: Error!
  
  const rejectedPromise = new Promise.reject((_, reject) => reject(new Error('Error!')));
  ```

  

- all

  모든 프로미스들이 fulfilled 상태가 되면 프로미스의 결과 값을 배열로 반환합니다. 각각의 작업들이 서로 연관되지 않을 때, 병렬적으로 수행할 수 있어 유용합니다. 작업 중에 하나라도 rejected가 되면 에러를 reject하는 프로미스를 반환합니다. 또한, 먼저 작업이 종료되더라도 반환 순서는 명시된 순서를 따릅니다.

  ```javascript
  const request1 = () => 
  	new Promise(resolve => setTimeout(() => resolve(1), 1000));
  const request2 = () => 
  	new Promise(resolve => setTimeout(() => resolve(2), 2000));
  const request3 = () => 
  	new Promise(resolve => setTimeout(() => resolve(3), 3000));
  
  Promise.all([request1(), request2(), request3()])
  	.then(console.log)
  	.catch(console.error);
  // [1,2,3]
  // 3초 소요
  ```

  

- race

  가장 먼저 fulfilled 상태가 된 프로미스의 처리 결과를 resolve합니다. all과 마찬가지로 하나라도 rejected 상태가 되면 그 즉시 에러 프로미스를 반환합니다.

  ```javascript
  Promise.race([
    new Promise(resolve => setTimeout(() => resolve(1), 1000)),
    new Promise(resolve => setTimeout(() => resolve(2), 2000)),
    new Promise(resolve => setTimeout(() => resolve(3), 3000))
  ])
  	.then(console.log) // 1
  	.catch(console.error);
  ```

  

- allSettled

  모든 프로미스들이 fulfilled나 rejected 상태가 되면 그 결과를 배열에 담아서 반환합니다. 성공했을 땐 상태와 값을, 실패했을 땐 상태와 에러를 담아서 보여줍니다.

  ```javascript
  Promise.allSettled([
    new Promise(resolve => setTimeout(() => resolve(1), 1000)),
    new Promise((_,reject) => setTimeout(() => reject(new Error('Error!')), 1000))
  ])
  	.then(console.log)
  /*
  [
  {status: "fulfilled", value: 1},
  {status: "rejected", reason: Error! at ~}
  ]
  */
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
// all
function pickAllData() {
    return Promise.all([getNum(), getChar()])
        .then(data => data.join(' + '));
}
pickAllData().then(console.log);
// race
function pickOnlyOne() {
    return Promise.race([getNum(), getChar()]);
}
pickOnlyOne().then(console.log); // 작업이 먼저 끝난 것만 보여줌
```



# Refference

> - https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise
> - https://www.youtube.com/watch?v=s1vpVCrT8f4&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=11
> - 모던 자바스크립트 Deep Drive - 위키북스