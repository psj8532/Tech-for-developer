### **선택기준**

**Angular**

-기능이 풍부하고 규모가 큰 애플리케이션을 개발할 때
-믿을 수 있고 확장 가능한 프레임워크가 필요할 때
-채팅 앱이나 메시징 앱과 같은 실시간 애플리케이션을 개발할 때
-장기프로젝트이며, 투자규모도 상당한 네이티브 앱이나 하이브리드 앱, 또는 웹앱을 개발할 때
-타입스크립트(TypeScript)로 코딩해야 할 때
-객체지향(Object-oriented)프로그래밍을 해야 할 때

 

**React**

-빠른 일정 안에 엔터프라이즈 수준의 가벼우면서도 현대적인 애플리케이션을 개발해야 할 때
-웹사이트 개발 솔루션을 안전하게 보호할 수 있는 유연한 프레임워크가 필요할 때
-크로스 플랫폼(cross-platform) 애플리케이션이나 싱글 페이지 애플리케이션(SPA)을 개발할 때
-기존의 앱에서 기능성을 확장할 때

-강력한 커뮤니티 지원과 솔루션이 필요할 때

 

**Vue**

-시장 진입 단계에서 필요한 프레임워크를 선택할 때
-작고 가벼운 애플리케이션을 개발할 때
-기존의 프로젝트에서 현대적이지만 제한된 리소스를 가진 프레임워크로 마이그레이션을 해야할 때
-기업이 아니라 사용자 커뮤니티의 지원을 받는 프레임워크를 원할 때

###  

### **차이점**

1. data 변이

   **Vue**

   data 객체에 있는 변수를 변경하려면 변수에 값을 할당하기만 하면 됐다. 즉, 자유롭게 업데이트가 가능하다는 것이다. 그 이유는 Vue에서 data 객체에 있는 변수가 업데이트되면 자동으로 setState를 쓴 것과 같이 자동으로 다 처리해주기 때문이다.

    

   **React**

   Reat의 state에 있는 data를 업데이트하려면 setState를 사용하는 것이 권장 된다. setState를 하지 않으면 특정 라이프 사이클 훅이 다시 실행되려고 하기 때문이다. 이는 React가 더 많은 작업을 해야함을 의미하기 때문에 setState를 사용하여 업데이트 해줌으로써 state의 값이 변경됐다는 것만 인지할 수 있도록 만들어준다.

2. 양방향 바인딩

   **Vue**

   v-model을 사용하여 양방향 바인딩을 한다. v-model에 입력된 키와 data가 자동으로 연결된다. input 필드는 data를 업데이트할 수 있고, data는 인풋필드를 업데이트 할 수 있다.

    

   **React**

   양방향 바인딩을 위해서는 유사한 함수를 만들어야한다. state에 있는 값을 input 필드에 반영하기 위해서는 value라는 속성을 이용해야한다. 또한, input 필드에 있는 값을 state에 있는 변수에 할당하기 위해서는 onChange이벤트를 걸어준다. event.target.value를 this.setState로 업데이트 해준다.

   ```
   handleInput = e => {
   	this.setState({
       	data: e.target.value,
       })
   }
   ...
   	<input type="text" value={this.state.data} onChange={this.handleInput}>
   ```

    

### 참고

> [blog.wishket.com/](http://blog.wishket.com/)[blog.wishket.com/%EC%95%B5%EA%B7%A4%EB%9F%AC-vs-%EB%A6%AC%EC%95%A1%ED%8A%B8-vs-%EB%B7%B0-%EC%96%B4%EB%96%A4-%EA%B2%8C-%EC%B5%9C%EA%B3%A0%EC%9D%98-%EC%84%A0%ED%83%9D%EC%9D%BC%EA%B9%8C/](http://blog.wishket.com/앵귤러-vs-리액트-vs-뷰-어떤-게-최고의-선택일까/)