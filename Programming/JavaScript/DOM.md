## DOM(Document Object Model)이란?

**HTML 문서의 계층적 구조와 정보를 표현**하며 이를 제어할 수 있는 API, 즉 **프로퍼티와 메서드를 제공하는 트리 자료구조**다.

HTML 요소는 렌더링 엔진에 의해 파싱되어 DOM을 구성하는 요소 노드 객체로 변환되고, 이러한 노드 객체들로 구성된 트리 자료구조가 DOM이다.



## 요소 노드 취득

#### Document.prototype.getElementById 

**인수로 전달한 id** 어트리뷰트 값을 갖는 **하나의 요소** 노드를 탐색하여 반환한다. Document.prototype의 프로퍼티이므로, 반드시 **document**를 통해 호출해야 한다. id는 고유한 값이므로 문서 내에 유일해야하지만, 중복되도 에러가 발생하지는 않는다. 만약, 중복된 id 값을 갖는 요소가 여러 개 일 경우, **첫번째 요소 노드만 반환**한다.

#### Document/Element.prototype.getElementsByTagName

인수로 전달한 태그 이름을 갖는 **모든 요소 노드들을 탐색하여 반환**한다.

#### Document/Element.prototype.getElementByClassName

인수로 전달한 class 어트리뷰트 값을 갖는 **모든 요소 노드들을 탐색하여 반환**한다.

#### CSS 선택자 이용

스타일을 적용하고자 할 때 사용한다.

**Document/Element.prototype.querySelector** 메서드는 인수로 전달한 css 선택자를 만족시키는 **하나의 요소 노드를 탐색하여 반환**한다.

- 여러 개인 경우, `첫번째 요소 노드만` 반환한다.
- 존재하지 않는 경우 `null`을 반환한다.
- css 선택자가 문법에 맞지 않는 경우, `DOMExeption 에러`가 발생한다.

**Document/Element.prototype.querySelectorAll** 메서드는 인수로 전달한 css 선택자를 만족시키는 **모든 요소노드를 탐색하여 반환**한다.

- 존재하지 않는 경우 `빈 NodeList 객체`를 반환한다.
- css 선택자가 문법에 맞지 않는 경우, `DOMExeption 에러`가 발생한다.

```javascript
const $apple = document.querySelector('.apple'); // 괄호 안에 css 선택자가 들어간다. // id: #, class .
```



css 선택자 문법을 사용하는 querySelctor, querySelctorAll은 getElemntBy''' 메서드에 비해 느리다. 하지만, css 선택자 문법을 사용하므로 좀 더 구체적인 조건으로 요소 노드를 취득할 수 있고 일관된 방식으로 취득할 수 있다는 장점이 있다. 따라서 **id 요소 노드를 취득하는 경우에는 속도가 빠른 getElementById를 사용**하고 **나머지는 querySelctor, querySelctorAll를 사용**하는 것이 좋다.



## HTMLCollection과 NodeList

HTMLCollection과 NodeList는 DOM API가 여러개의 결과 값을 반환하기 위한 DOM 컬렉션 객체다. 이 둘은 모두 유사 배열 객체이면서 이터러블이므로 for ... of로 순회할 수 있고, 스프레드 문법을 사용하여 배열로 변환할 수 있다.

#### 문제점

이 둘은 노드 객체의 상태 변화를 실시간으로 반영하는 살아있는 객체이다. HTMLCollection의 경우 언제나 live 객체로 동작한다. NodeList는 대부분의 경우 과거 정적 상태를 유지하는 non-live 객체로 동작하지만, live 객체로 동작할 때가 있다. HTMLCollection을 반환하는 getElementByTagName, getElementByClassName 메서드를 사용할 때, for 문을 순회하면서 값이 동적으로 바뀜에 따라 원하는 결과가 나오지 않는다.

#### 해결 방법

HTMLCollection이나 NodeList 객체를 배열로 변환하여 사용하여 위와 같은 문제를 해결할 수 있다. 또한, 배열의 경우 유용한 고차함수(forEach, map, filter, reduce 등)를 사용할 수 있어 편리하다.



## 노드 탐색

#### 자식 노드 탐색

| 프로퍼티                            | 설명                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| Node.prototype.childNodes           | 자식 노드 모두 탐색하여 NodeList에 담아 반환한다. 요소 노드와 텍스트 노드 모두 포함된다. |
| Element.protorype.children          | 자식 노드 중에서 요소 노드만 모두 탐색하여 HTMLCollection에 담아 반환한다. |
| Node.prototype.firstChild           | 첫번째 자식 노드만 반환한다. 텍스트 노드와 요소 노드 모두 포함된다. |
| Node.prototype.lastChild            | 마지막 자식 노드만 반환한다.                                 |
| Element.protorype.firstElementChild | 첫번째 자식 요소 노드를 반환한다. 요소 노드만 반환한다.      |
| Element.protorype.lastElementChild  | 마지막 자식 요소 노드를 반환한다.                            |



## 요소 노드의 텍스트 조작

#### nodeValue

- `getter`와 `setter` 모두 존재하므로 **참조와 할당 모두 가능**하다.
- 참조할 경우, 노드객체의 값을 반환한다. 즉, **텍스트노드의 텍스트**이다. 다른 노드의 경우엔 null을 반환한다.

#### textContent

- `getter`와 `setter` 모두 존재하므로 **참조와 할당 모두 가능**하다.
- 요소 노드의 텍스트와 모든 자손 노드의 텍스트를 취득하거나 변경한다.
- 마크업은 무시된다.

- 만약 요소 노드의 콘텐츠 영역에 자식 노드가 없고 텍스트만 존재한다면 textContent를 쓰는 것이 더 간단하다.

#### ※ innerText

textContent와 유사하나 사용하지 않는 것이 좋다.

- css에 순종적이기 때문에 css에 의해 비표시로 지정된 요소 노드의 텍스트는 반환하지 않는다.
- css를 고려해야 하므로 textContent 프로퍼티보다 느리다.

