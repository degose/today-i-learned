## React, Angular, Vue.js


### React
* React는 MVC 패턴에서 V를 담당하는 라이브러리이며, 리덕스나 리액트 라우터를 사용하면서 MVC 패턴을 유사하게 만들 수 있다.
* JSX
    * 꼭 루트 노드가 필요하다 -> React16부터는 배열처럼 하나하나씩 줄 수 있으나 각각의 key 값이 필요
    * 속성명은 자바스크립트처럼 camelCase, 태그 안에 내용이 없는 경우 />를 사용
    * if문 대신에 삼항 연산자를 사용
* Props
    * 부모 컴포넌트로부터 물려받는 속성.
    * 부모 컴포넌트에서 전달하는 props가 바뀌면 자동으로 업데이트
* defultProps
    * 만약 부모 컴포넌트에서 따로 속성을 넘겨주지 않는다면 자동으로 defultProps가 적용된다.
* propTypes
    * PropTypes 객체는 prop-types 패키지를 따로 설치해야 쓸 수 있다.
    * React의 props 자료형 검사법
    * isRequired는 필수라는 뜻 -> 이것을 붙여주면 반드시 있어야 한다라는 것
* state
    * constructor(){ this.state={ hidden: false };}
    * state는 컴포넌트가 만들어질 때 가장 먼저 설정되는 것이기 때문에 constructor 안에 적어준다.
    * state는 해당 컴포넌트에만 사용되는 상태
    * props처럼 자동으로 업데이트된다.
* setState
    * state 설정 메소드
    * `this.state.이름 = 바꿀값;`이 아니라 `this.setState((이전 상태) => ({이름: 바꿀 값}));`
    * setState의 콜백함수는 매개변수로 이전상태를 제공한다.
* 이벤트 바인딩
    * constructor 안에 `this.onClickButton = this.onClickButton.bind(this);`
    * 바인딩 시켜주지 않으면, render 메소드에서 this.onClickButton 함수를 호출했을 때 함수의 this가 window나 undefined가 되어버린다. 그래서 window 나 undefined에는 setState 메서드가 없으므로 에러를 발생시킨다.
    * arrowfunction을 쓰면 this를 알아서 바인딩 시켜주기 때문에 이것을 쓰는것이 좋다.
* static 키워드
    * 정적 메소드 정의
    * 인스턴스를 생성하지 않고 사용할 수 있는 메소드.
    * 정적메소드는 prototype에 추가되지 않는다.
* class
    * 클래스의 선언부 let, const 모두 호이스팅은 되지만 일시적 사각지대에 빠져 레퍼런스 에러를 발생시킨다.
    * 클래스의 코드는 ‘use strict’를 선언하지 않아도 strict 모드에서 실행된다.
    * 메서드를 작성할 때 function 키워드와 콜론을 작성하지 않는다.
    * 메서드 사이에 콤마를 작성하지 않는다.
* extends
    * 클래스 간의 상속이 가능해졌다.
    * 상속받은 클래스(슈퍼클래스)의 메소드를 사용할 수 있다.
    * 슈퍼클래스의 메소드를 오버라이딩 할 수 있다.
    * super키워드를 통해 접근 가능
* constructor
    * 서브클래스에서 정의된 constructor가 없으면 슈퍼 클래스의 constructor가 호출 된다.
    * 서브클래스에서 constructor를 정의 하려면 반드시 constructor 내부에서 super()를 호출해야 한다.

* 생명주기
    * Mount
        * 컴포넌트가 처음 실행될 때 
        * 컴포넌트 시작 -> context, defaultProps, state 저장 -> componentWillMount 메소드 호출 -> render로 컴포넌트를 DOM에 부착 -> Mount 완료 -> componentDidMount 호출
        * componentWillMount에서는 props나 state를 바꾸면 안된다. Mount 중이므로 아직 DOM에 render 하지 않았기 때문에 DOM에도 접근 불가능
        * componentDidMount 에서는 DOM에 접근 가능 그래서 여기에서는 주로 AJAX 요청, setTimeout, setInterval 같은 행동을 한다.
    * Props Update
        * props가 업데이트될 때의 과정
        * 업데이트 되기전 업데이트 발생감지 -> 
        * componentWillReceiveProps 메소드 호출 ->
        * shouldComponentUpdate -> 
        * componentWillUpdate ->
        * 업데이트 완료(render) ->
        * componentDidUpdate
        * 이 메소드들은 첫번째 인자로 바뀔 props 에 대한 정보를 가지고 있다.
        * componentDidUpdate만 이미 업데이트 되었기 때문에 바뀌기 이전의 props에 대한 정보를 가지고 있다.
        * shouldComponentUpdate 에서는 아직 render 하기 전이기 때문에 return false를 하면 render 를 취소할 수 있다. -> 성능 최적화를 한다. -> 쓸데없는 update가 일어나면 여기서 걸러낸다.
        * componentWillUpdate 에서는 state 를 바꿔서는 안된다. 아직 props도 업데이트하지 않았으르모 state를 바꾸면 또 shouldComponentUpdate가 발생
        * componentDidUpdate에서는 render가 완료되었기 때문에 DOM에 접근 가능
    * State Update
        * setState를 통해 state가 업데이트 될 때의 과정
        * props update와 과정이 같지만 componentWillReceiveProps 메소드는 호출되지 않는다.
        * 메소드의 두번째 인자로는 바뀔 state에 대한 정보를 가지고 있다.
        * componenetDidUpdate는 두번째 인자로 바뀌기 이전의 state에 대한 정보를 가지고 있다.
    * Unmount
        * 컴포넌트 제거. 더는 컴포넌트를 사용하지 않을 때 발생하는 이벤트
        * componentWillUnmount => componentWillMount에서 연결했던 이벤트 리스너를 제거하는 등의 활동
    * Error
        * componentDidCatch
* 리액트 라우터
    * 새로고침없이 하나의 페이지만으로 동작하는 SPA가 유행했지만, 주소가 없으므로 특정 페이지에 접속하기 힘들고 북마크를 할 수 없다는 단점이 있었다.
    * 리액트 라우터를 사용하면 싱글 페이지 애플리케이션과 같이 페이지 새로고침 없으면서도 주소를 가질 수 있게 된다. 
    * SPA의 단점은 자바스크립트 번들 파일에 어플리케이션에 대한 모든 로직을 불러와서, 규모가 커지면 용량이 커지기 때문에, 로딩속도가 지연될 수 있다. => 필요에 따라 번들 파일을 여러개의 파일로 분리시키는 코드 스플리팅으로 해결
    * 그러나 검색엔진 최적화는 안되므로 부분적으로 서버사이들 렌더링을 해줄 필요가 있다.
    * browserHistory -> 일반 웹을 사용하는 것처럼 주소를 바꾸고, 뒤로가기와 앞으로가기를 할 수 있다.
    * indexRoute -> /에 해당하는 path에 기본으로 보이는 컴포넌트
    * this.props.children 속성으로 App 컴포넌트로 전달
* 리덕스
    * MVC 패턴을 대체하기 위해 Flux 패턴을 살짝 바꾼 것
    * 경로
        * View -> Action -> Dispatcher -> Store(Middleware -> Reducer) -> View
        * UI -> Actions -> Reducer -> Store -> State -> UI
    * 한 방향으로만 흐르기 때문에 데이터의 흐름을 예측하기 쉽다. -> 관리하기 쉽다.
    * 함수형 프로그래밍을 따르기 때문에 불변하여 예측하기 쉽고, 이전 상태로 되돌리기도 쉽다.
    * 예
        * 로그인 버튼, 폼 화면(View화면에 Action을 연결해 둠) Action은 그냥 로그인이라는 동작을 정의해 둠 -> 
        * Dispatcher를 통해서 Action에서 Store로 데이터가 넘어감(Dispatcher는 아까 정의해 둔 로그인 Action을 실행하는 부분) -> 
        * Store에는 Middleware, Reducer 가 있다. (Reducer는 데이터를 처리하는 부분 / Middleware는 Reducer에 가기 전 Action을 조작) ->
        * 처리된 데이터를 다시 View로 넘겨준다.
    * State
        * 데이터
        * React state와는 다름. 웹앱 전체의 상태를 관리하기 때문
        * 각각의 컴포넌트는 리덕스에서 저장된 state를 읽어봐 사용
    * react-redux
        * 리액트에서 리덕스 패턴을 사용할 수 있게 해주는 패키지
        * redux 패키지도 같이 설치해 주어야 함
        * connect
            * redux와 react가 소통하는 부분
            * redux의 state가 mapStateToProps 함수를 통해 React의 props로 전달(Store -> View)
            * Store에서 바뀐 정보가 View로 가는 것
        * action
            * 대문자로 표기
            * login함수를 dispatch하는 순간 Store에게 Action이 전달
            * login컴포넌트의 handleSubmit 안에 dispatch하는 부분이 들어있어서 폼을 submit 하면 dispatch메소드가 실행되는 것
            * Store로는 로그인을 처리하는 스토어를 만들어 두는데 reducer가 여기에 들어간다. reducer를 먼저 만들고 Store에 연결해준다.
            * reducer는 아까 만든 Action별로 어떻게 state를 바꿀지 결정
            * 주의!!!! 반드시 새로운 객체를 반환해야 한다. `...state`로. -> 현재와 이전 상태가 구분되기 때문에 이전 상태로 쉽게 되돌릴 수 있다.
            * defaltState 가 기본 state
            * Reducer에서 이 state만 조작해서 정보를 표현해야한다.
            * 어차피 Store과 View는 연결되어 있기 때문에 state만 바꾸면 알아서 View도 바뀐다.
            * Reducer는 여러 개를 사용할 수 있기 때문에 redux패키지로부터 combineReducers함수를 불러와서 합쳐준다.
        * configureStore.js
            * reducer와 Store를 연결할 때 필요
            * Store에서는 Node.js처럼 미들웨어를 사용할 수 있다.
            * Store에 Action이 넘어갈때마다 미들웨어를 거친다.
    * Container, Component
        * Container도 react패키지의 Componenet를 물려받는 컴포넌트의 일종
        * container는 리덕스와 소통하면서 앱의 상태(리덕스 state)를 제어하는 컴포넌트
        * container는 앱의 상태를 관리하기 때문에 앱의 상태가 자주 바뀔수록 그에 따라 빈번하게 업데이트가 일어남.
        * container는 리덕스로부터 데이터를 받고 action을 실행하는 역할만 전담
        * component는 리덕스의 state가 어떻든 상관하지 않고 사용자오 상호작용한 후 로그인 정보를 받아서 container로 넘겨준다.
        * 각각 자신의 역할이 명확하기 때문에 어떤 에러가 발생했을 시 어떤 컴포넌트를 고쳐야하는지 확인하기 쉽다.
        * 불필요한 컴포넌트의 업데이트를 방지할 수 있어 성능이 좋아진다.