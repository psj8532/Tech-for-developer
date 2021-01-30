## this란?

자신이 속한 객체나 또는 자신이 생성할 인스턴스를 가리키는 **자기 참조 변수**다. this를 사용하면 자신이 속한 객체나 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있다. this 바인딩은 this와 this가 가리킬 객체를 바인딩 하는 것을 의미한다.



## 생성 시기

**렉시컬 스코프**는 함수가 정의될 때 생성된다. 하지만 **this**는 정의와 상관없이 <u>호출될 때</u> 생성된다. 즉, this 바인딩은 함수가 어떻게 호출됐는지에 따라 동적으로 결정된다.



## 호출 방식에 따른 this 바인딩 값

### 일반 함수 호출

> 전역 객체

일반 함수 호출을 사용하면 함수가 어디에 정의되있든 내부 this가 전역 객체를 가리킨다.

```javascript
var v = 10;

const obj = {
  v: 100,
  foo() {
    setTimeout(() => console.log(this.v), 1000);
  }
}

obj.foo();
// 10
```

#### 해결 방법

##### 화살표 함수 사용

```javascript
// 화살표 함수 내부의 this는 상위 스코프의 this를 가리킨다.
var v = 10;

const obj = {
  v: 100,
  foo() {
    setTimeout(() => console.log(this.v), 1000);
  }
}

obj.foo();
// 100
```

##### this 바인딩을 변수에 할당

```javascript
// this 바인딩을 that에 할당
var v = 10;

const obj = {
  v: 100,
  foo() {
    const that = this;
    setTimeout(() => console.log(that.v), 1000);
  }
}

obj.foo();
// 100
```



### 메서드 호출

> 메서드를 호출한 객체

메서드 내부의 this는 메서드를 호출한 객체를 바인딩한다. 즉 메서드를 호출할 때, 메서드 이름 앞의 마침표 연산자 앞에 기술한 객체가 바인딩된다.

```javascript
const fruit = {
  name = 'banana';
  getName() {
    return this.name;
  }
}

console.log(fruit.getName()); // banana
```



### 생성자 함수 호출

> 생성될 인스턴스

생성자 함수가 생성할 인스턴스를 가리킨다.

```javascript
const Fruit(fruit) {
  // this는 생성된 인스턴스에 바인딩 되있다.
  this.name = fruit;
  getName() {
    return this.name;
  }
}

const fruit1 = new Fruit('apple'); // apple
const fruit2 = new Fruit('pineapple') // pineapple
```





### Function.protype.apply/call/bind 메서드에 의한 간접 호출

##### apply

##### call



##### bind

```javascript
const fruit = {
  name: 'apple',
  foo(callback) {
    setTimeout(callback.bind(this), 100);
  }
  /*
  foo(callback) {
    setTimeout(callback, 100); //  is fruit
  }
  */
};

fruit.foo(function () {
  console.log(`${this.name} is fruit`); // apple is fruit.
})
```





|             함수 호출 방식              |            this 바인딩             |
| :-------------------------------------: | :--------------------------------: |
|             일반 함수 호출              |             전역 객체              |
|               메서드 호출               |        메서드를 호출한 객체        |
|            생성자 함수 호출             |   생성자 함수가 생성할 인스턴스    |
| Apply/call/bind 메서드에 의한 간접 호출 | 메서드에 첫번째 인수로 전달한 객체 |



#### 참고

> 모던 자바스크립트 Deep Drive

