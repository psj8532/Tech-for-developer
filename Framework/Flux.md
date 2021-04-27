## Flux의 등장

오늘날 많이 쓰이는 `redux`와 `vuex`는 `flux 패턴`을 기반으로 만들어진 `상태 관리 라이브러리`이다. 규모가 큰 프로젝트에서 상태 관리를 효율적으로 할 수 있도록 도와준다. 그렇다면 이러한 flux 패턴은 어떻게 만들어진 것일까?

flux는 facebook에서 `클라이언트-사이드 웹 애플리케이션`을 위해 만든 애플리케이션 아키텍쳐다. 기존에 사용하던 <u>MVC 패턴의 한계</u> 때문이다. 기존 MVC 패턴에서는 Model과 View가 `양방향 바인딩`으로 연결됐습니다. Controller를 이용하여  Model에 `CRUD`를 하고, View에서 Model에 접근하여 데이터를 가져오는 형태입니다. 만약 프로젝트의 규모가 커지고 복잡해진다면 Model을 변경하고 이 Model을 참조하는 View에서 다시 변경된 데이터를 받아와야합니다. 이러한 문제점을 개선하고자 만든 것이 `flux 패턴`입니다.



## 구조

![Flux 구조](https://haruair.github.io/flux/img/flux-simple-f8-diagram-1300w.png)

![](https://haruair.github.io/flux/img/flux-simple-f8-diagram-with-client-action-1300w.png)

Flux는 `단방향 데이터` 흐름을 가지고 있습니다. 먼저, `Action` 이벤트를 dispatcher에게 알립니다. 그리고 `dispathcer`는 해당하는 store에 payload를 전달합니다. `store`는 스스로 갱신한 다음 자신이 변경됐다는 사실을 모두에게 알립니다. `controller-view`는 이 이벤트를 듣고 새로운 데이터를 store에서 가져와 모든 자식 view에게 뿌려줍니다.



## 구성

### Action

데이터를 변경하면 action을 통해 action 타입과 변경된 데이터를 dispatcher에게 전달합니다.



### Dipatcher

dispatcher는 애플리케이션의 `중앙 허브`입니다. <u>모든 데이터의 흐름을 관리</u>합니다. action의 type을 확인하고 필요한 store로 액션과 페이로드를 전달합니다. dispatcher는 `의존성 관리`도 할 수 있습니다. 해당 데이터가 쓰이는 store가 두개이고 store2가 store1을 의존하고 있다고 가정해보겠습니다. store2가 먼저 진행된다면 store1에서 변경된 값을 활용할 수 없고 이는 동기화가 제대로 되지 않는 현상으로 이어질 수 있습니다. 따라서 store1이 완료될 때까지 기다려야 합니다. flux는 `waitFor()` 메서드를 제공하여 이를 가능하게 해줍니다.



### Store

store는 애플리케이션의 `상태`, `로직`을 포함하고 있습니다. 단순히 ORM 스타일의 객체 컬렉션 관리를 넘어 애플리케이션 내의 `개별적인 도메인`에서 애플리케이션의 상태를 관리합니다. 

store는 자신을 dispatcher에 등록하고 action을 parameter로 받는 callback을 제공합니다. Callback 내부에서는 switch 문을 활용해서 action의 type 별로 분류하고 store 내부 메서드와 연결할 수 있는 훅을 제공합니다. 즉, action은 dispatcher를 통해 store를 갱신하는 것입니다. Store 업데이트 후, 상태 변경을 알려 하위 view에 뿌려주고 스스로 업데이트 할 수 있게 합니다.



### View

React에서 재 렌더링을 제공하는 또 다른 view입니다. 이 view를 `controller-view` 라고 부릅니다. controlle-view는 store에게 이벤트를 받으면 store의 `public getter` 메서드를 통해 새로 필요한 데이터를 요청합니다. 그 과정에서 `setState()` 또는 `forceUpdate()`를 호출합니다. 다시 이 과정에서 자체 `render()` 메서드와 모든 하위에 있는 `render()` 메서드를 실행합니다. 이후, view는 새로운 값으로 렌더링 되는 것입니다.



## 결론

Redux와 Vuex는 Flux 기반이긴 하지만 Flux와 같다고는 할 수 없습니다. Flux와 함수형 프로그래밍 등 다른 요소들을 섞어서 만든 것이기 때문입니다. 하지만 기본적인 원리는 Flux와 동일합니다. 따라서 상태 관리에 있어서 유용합니다.



#### 참고

- https://haruair.github.io/flux/docs/overview.html
- https://www.huskyhoochu.com/flux-architecture/