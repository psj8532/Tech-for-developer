## 개념

- 인덱스를 가지는 자료구조
- 데이터는 순차적으로 저장되며 중복 가능
- 인덱스를 이용하여 접근 가능



## APIs

### 생성

- new

```javascript
let fruits = new Array(2); // 길이 2만큼의 빈 슬롯을 가진 배열
```

- 리터럴 표기법(literal notation)

```javascript
let fruits = ['사과', '바나나']; // ['사과', '바나나'] 배열 생성
```



### 추가

**concat**

- 기존 배열 변경 x (복사만 해옴)
- 새로운 배열 반환

```javascript
arr = ['banana'];
const newArray = arr.concat('apple');

console.log(arr); // ['banana']
console.log(newArray); // ['banana', 'apple']
```

**push**

- 기존 배열의 끝에 요소 추가 (원본 변경)
- 배열의 새로운 길이 반환

```javascript
arr = ['banana'];
const newArray = arr.push('apple');

console.log(arr); // ['banana', 'apple']
console.log(newArray); // ['banana', 'apple']
```

=> 원본을 건드리지 않는 `concat`을 사용하는 것이 좋다!!

 

### 삭제

**pop**

- 배열의 맨 뒤에 있는 요소 하나를 제거

```javascript
arr = [1,2,3,4,5];
arr.pop();
console.log(arr); // [1,2,3,4]
```

**slice**

- 원본 변경 x
- begin부터 end까지에 대한 얕은 복사로 새로운 배열 객체 반환
- 음수를 지정하면 뒤에서 부터 셈
- slice(start[, end])

```javascript
arr = [1, 2, 3, 4, 5];
// 삭제하려는 인덱스: idx
const newArray = arr.slice(0,idx).concat(arr.slice(idx,5));

console.log(arr); // [1,2,3,4,5]
console.log(newArray); // [1,2,4,5]
```

**splice**

- 원본 변경
- 배열의 기존 요소를 삭제 또는 교체하거나 새로운 요소를 추가하여 배열의 내용 변경
- splice(start[, deleteCount[, item1[, item2[, ...]]]])
```javascript
arr = [1, 2, 3, 4, 5];
// 삭제하려는 인덱스: [0],[1],[2]
const newArray = arr.splice(0,3,10,11);

console.log(arr); // [10,11,4,5]
console.log(newArray); // [10,11,14,5]
```

**filter**

- 조건을 만족하는 요소를 모아 새로운 배열로 반환

```javascript
arr = [1, 2, 3, 4, 5];
// 삭제하려는 인덱스: idx
const newArray = arr.filter((v,i) => i !== idx);

console.log(arr); // [1,2,3,4,5]
console.log(newArray); // [1,2,4,5]
```

 

### 반복문

**entries**

- 배열의 각 인덱스를 키,값 쌍 형태의 새로운 Array Iterator 객체를 반환

```javascript
var arr = ['a','b','c'];

for (const [idx, val] of arr.entries()) {
    console.log(idx, val);
}
// 0 'a'
// 1 'b'
// 2 'c'
```

**for...of**

```javascript
var a = ['a','b','c'];
var arr = a.entries();

for (let e of arr) {
    console.log(e);
}
// [0, 'a']
// [1, 'b']
// [2, 'c'] 
```

**for each**

-  for문과 마찬가지로 반복적인 기능을 수행
- 하지만 for문처럼 index와 조건식, 증감식를 정의하지 않아도 callback 함수를 통해 기능 수행

```javascript
const arr = [0,1,2,3,4];

arr.forEach(function(element,index,array?){
	console.log(index, element);
});

arr.forEach((element,index) => console.log(element,index));
```

**for**

```javascript
const arr = ['a','b','c'];
for (var i=0; i<arr.length; i++) {
    console.log(i,arr[i]);
}
```

**map**

- 배열의 모든 요소를 주어진 함수 넣고 결과를 모아 새로운 배열 반환

```javascript
const array1 = [1, 4, 9, 16];
// pass a function to map
const map1 = array1.map(x => x * 2);
console.log(map1);
// expected output: Array [2, 8, 18, 32]
```



### 탐색

**find**

- 판별 함수를 만족하는 첫 번째 요소 값 반환

```javascript
const array1 = [5, 12, 8, 130, 44];
const found = array1.find(element => element > 10);
console.log(found);
// expected output: 12
```

**findIndex**(=indexOf)
- 판별 함수를 만족하는 첫번째 요소의 인덱스

```javascript
const array1 = [5, 12, 8, 130, 44];
const isLargeNumber = (element) => element > 13;
console.log(array1.findIndex(isLargeNumber));
// expected output: 3
```


**lastIndexOf**

- 찾고자 하는 값을 가진 인덱스 중에서 가장 마지막에 있는 인덱스


### 문자열 <=> 배열

**join** (배열 => 문자열)

**split** (문자열 => 배열)


### 역순
**reverse**

### 추출
**find**
**filter**

### 변환
**map**

### 조건
**some**
- 조건을 만족하는 요소가 하나라도 있다면 true, 없으면 false 리턴

**every**

- 모든 요소가 조건을 만족해야만 true 리턴 

### 누적 
**reduce**
```javascript
const result = students.reduce((prev,cur) => {
  console.log('-----');
  console.log('prev');
  console.log('cur');
  return cur
}, 0);
// ----
// 0
// 첫번째 요소
// ----
// 첫번재 요소
// 두번째 요소
```