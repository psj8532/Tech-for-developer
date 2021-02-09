#### DOM manipulation이란?

**새로운 노드를 생성하여 DOM에 추가**하거나 **기존 노드를 삭제 또는 교체**하는 것을 말한다.



## innerHTML

**setter**와 **getter** 모두 존재하는 접근자 프로퍼티이다. 요소 노드의 콘텐츠 영역 내에 포함된 모든 HTML 마크업을 **문자열**로 반환한다.

### 장점

- 구현이 간단하고, 직관적이다.

### 단점

- 사용자의 인풋 값을 그대로 innerHTML 프로퍼티에 할당하면 **크로스 사이트 스크립팅 공격**에 취약하다. 악성코드가 포함된 자바스크립트 코드가 포함됐다면 파싱 과정에서 그대로 실행되기 때문이다. 
- innerHTML은 **할당하기 전에 요소의 모든 자식 노드를 제거**한다. **이후, 할당한 문자열을 파싱하여 DOM에 추가**한다. 만약, 이미 여러 자식 노드를 가지고 있는 요소 노드에 자식 요소 하나를 추가하고자 할때, 기존 자식 요소는 변경할 필요가 없지만, 이를 모두 제거하고 다시 할당하기 때문에 성능면에서 좋지 않다.

-  새로운 요소의 삽입 위치를 지정할 수 없다. 만약, 여러 자식 노드들 중에서 특정 위치에 삽입하고 싶을 때도, 모든 자식 노드들을 제거한 후 재할당해야한다.



## insertAdjacentHTML

### 장점

- 특정 위치에 삽입 가능하기 때문에, innerHTML에 비해 효율적이다. 즉, 기존 요소에 영향을 주지 않고, 새롭게 삽입될 요소만 파싱하여 자식노드에 추가할 수 있다.

### 단점

- innerHTML과 마찬가지로 HTML 마크업을 포함하고 있기 때문에 **크로스 사이트 스크립팅 공격**에 취약하다.

```html
<!-- beforebegin -->
<div id="foo">
  <!-- afterbegin -->
  text
  <!-- beforeend -->
</div>
<!-- afterend -->
```

Element.prototype.insertAdjacentHTML(position, DOMString)



## 노드 생성, 추가

```javascript
const $fruits = document.createElement('ul');
```

##### 요소 노드 생성

```javascript
const $li = document.createElement('li');
```

##### 텍스트 노드 생성

```javascript
const textNode = document.createTExtNode('melon');
```

##### 텍스트 노드를  요소 노드의 자식 노드르 추가

```javascript
$li.appendChild(textNoe);
```

만약 요소 노드에 자식 노드가 없을 경우 위 방법보다 textContent 프로퍼티를 사용하는 편이 더욱 간편하다.

```javascript
$li.textContent = 'melon';
```

##### 요소 노드를 DOM에 추가

```javascript
$fruits.appendChild($li);
```



## 복수의 노드 생성과 추가

```javascript
const $fruits = document.getElementById('ul');
['banana', 'melon', 'apple'].forEach(fruit => {
  const $li = document.createElement('li');
  const textNode = document.createTextNode(fruit);
  $li.appendChild(textNode);
  $fruits.appendChild($li);
});
```

위 코드의 경우 DOM에 3번 추가하기 때문에 DOM이 3번 변경되고, 리플로우와 리페인트도 3번 실행된다. DOM을 변경하는 작업은 최소한으로 줄이는 것이 성능 향상에 도움이 된다.

해결 방법으로는 **컨테이너 요소**의 사용이 있다.

```javascript
const $fruits = document.getElementById('ul');
const $container = document.createElement('div');
['banana', 'melon', 'apple'].forEach(fruit => {
  const $li = document.createElement('li');
  const textNode = document.createTextNode(fruit);
  $li.appendChild(textNode);
  $container.appendChild($li);
});
$fruits.appendChild($container)
```

위 방법은 DOM이 한번만 변경되긴되지만 container로 사용한 div 태그도 같이 추가되는 단점이 있다. 이러한 문제는 **DocumentFragment** 를 사용하면 해결할 수 있다.

```javascript
const $fruits = document.getElementById('ul');
const $fragment = document.createDocumentFragment();
['banana', 'melon', 'apple'].forEach(fruit => {
  const $li = document.createElement('li');
  const textNode = document.createTextNode(fruit);
  $li.appendChild(textNode);
  $fragment.appendChild($li);
});
$fruits.appendChild($fragment);
```

DocumentFragment를 사용하여 기존 DOM에 추가하면 자신을 제외한 자식 노드만 DOM에 추가하기 때문에 효율적이다.



## 노드 삽입

##### 마지막 노드로 추가

Node.prototype.appendChild

##### 지정한 위치에 노드 삽입

Node.prototype.insertBefore(newNode, childNode)



## 노드 이동

DOM에 이미 있는 요소를 다시 추가하면 현재 위치에 있는 노드를 제거하고 새로운 위치에 노드를 추가한다.



## 노드 복사

Node.prototype.cloneNode([deep: ture | false])

deep copy: 자손 노드가 모두 포함된 사본 생성

Shallow copy: 노드 자신만의 사본 생성



## 노드 교체

Node.prototype.replaceChild(newChild, oldChild)



## 노드 삭제

Node.prototype.removeChild(child)