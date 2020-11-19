### 추가

**concat**

```
arr = ['banana'];
const newArray = arr.concat('apple');

console.log(arr); // ['banana']
console.log(newArray); // ['banana', 'apple']
```

 

**push**

```
arr = ['banana'];
const newArray = arr.push('apple');

console.log(arr); // ['banana', 'apple']
console.log(newArray); // ['banana', 'apple']
```

 

**차이점**

concat은 기존에 있는 배열을 복사해와서 연결한다. 이렇게하면 연결하기 전 배열의 상태는 유지한 채로 로 새로운 배열을 만들 수 있다. 반면에 push는 기존의 배열에 추가를 한채로 넘겨주기 때문에 원본의 값이 바뀌는 결과를 낳게 된다. 따라서, concat을 사용하는 것이 좋다.

 

### 삭제

**slice**

```
arr = [1, 2, 3, 4, 5];
// 삭제하려는 인덱스: idx
const newArray = arr.slice(0,idx).concat(arr.slice(idx,5));

console.log(arr); // [1,2,3,4,5]
console.log(newArray); // [1,2,4,5]
```

 

**filter**

```
arr = [1, 2, 3, 4, 5];
// 삭제하려는 인덱스: idx
const newArray = arr.filter((v,i) => i !== idx);

console.log(arr); // [1,2,3,4,5]
console.log(newArray); // [1,2,4,5]
```

 