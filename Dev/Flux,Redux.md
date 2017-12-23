## Flux & Redux

## Flux
- Facebook에서 클라이언트-사이드 웹 어플리케이션을 만들기 위해 사용하는 어플리케이션 아키텍쳐
- 단방향 데이터 흐름을 활용해 뷰 컴포넌트를 활용하는 React를 보완하는 역할
- `Dispatcher`, `Store`, `Views(React컴포넌트)`
- `controller-view` : stores에서 데이터를 가져와 그 데이터를 자식에게 보내는 역할
- `dispatcher`를 돕는 `action creator`메소드는 이 어플리케이션에서 가능한 모든 변화를 표현하는 유저의 API를 지원하는데 사용된다.

### 단방향 데이터 흐름
#### MVC 패턴의 단점
- 예를 들어 상단 바에 읽지않은 메세지를 표시하면서도 읽지 않은 메세지 수를 표시하고 싶을 때
- 메세지를 읽기 위한 단일 쓰레드에서 메세지 쓰레드 모델을 갱신해야하고 동시에 읽지 않은 메세지 수 모델을 갱신 해야하기 때문에 MVC 애플리케이션에서 다루기가 쉽지 않다.
- MVC 애플리케이션에서 종종 나타나는 데이터 간의 의존성과 연쇄적인 갱신은 뒤얽힌 데이터 흐름을 만들고 예측할 수 없는 결과로 이끌게 된다.

#### Flux의 store
- React view에서 사용자가 상호작용 ->
- view는 중앙의 dispatcher를 통해 action을 전파한다. ->
- 어플리케이션의 데이터와 비즈니스로직을 가지고 있는 store는 action이 전파되면 이 action에 영향이 있는 모든 view를 갱신한다.

- Flux의 store는 독립적인 세계를 가지고 있어 setAsRead()같은 직접적인 setter 메소드가 없는 대신 dispatcher에 등록한 콜백을 통해 데이터를 받게된다.
- store는 바깥에 아무것도 두지 않는 방식으로 데이터의 도메인을 관리해야 할 필요가 없어져 외부의 갱신에 따른 문제를 명확하게 분리할 수 있도록 돕는다.

#### 구조와 데이터 흐름
- Action -> Dispatcher -> Store -> View -> Action -> Dispatcher ...
- dispatcher, store 와 view는 독립적인 노드로 입력과 출력이 완전히 구분된다.
- action은 새로운 데이터를 포함하고 있는 간단한 객체로 type 프로퍼티로 구분할 수 있다.

- Action creator 는 라이브러리에서 제공하는 도움 메소드로 메소드 파라미터에서 action을 생성하고 type을 설정하고나 dispatcher에게 제공하는 역할을 한다.
  - actions/index.js
  ```js
  import axios from 'axios';

  const API_KEY = '90474bb0c07da94ad9b45f28533901c1';
  const ROOT_URL = `http://api.openweathermap.org/data/2.5/forecast?appid=${API_KEY}`;

  export const FETCH_WEATHER = 'FETCH_WEATHER';
  // 왜 문자열로 하지 않고 따로 변수를 만들어서 가져왔을까? => 액션 생성자와 리듀서 사이에 액션 타입을 계속 일정하게 유지하기 위해

  // API리퀘스트 날씨정보 가져오기
  export function fetchWeather(city) {
    const url = `${ROOT_URL}&q=${city},us`;
    const request = axios.get(url);
    
    // console.log('Request:', request);

    return {
      type: FETCH_WEATHER,
      payload: request
    };
  }
  ```
- 모든 action은 store가 dispatcher에 등록해둔 콜백을 통해 모든 store에 전송된다.
- action에 대한 응답으로 store가 스스로 갱신을 한 다음에는 자신이 변경되었다고 모두에게 알린다.
- controller-view라고 불리는 특별한 view가 변경 이벤트를 듣고 새로운 데이터를 store에서 가져온 후 모든 트리에 있는 자식 view에게 새로운 데이터를 제공한다.

- 양방향 데이터 바인딩은 연속적인 갱신이 발생하고 객체 하나의 변경이 다른 객체를 변경하게 되어 실제 필요한 업데이트보다 더 많은 분량을 실행하게 된다.
- 어플리케이션의 규모가 커지면 데이터의 연속적인 갱신이 되는 상황에서는 사용자 상호작용의 결과가 어떤 변화를 만드는지 예측하기 어려워진다.
- 갱신으로 인한 데이터 변경이 단 한차례만 이루어진다면 전체 시스템은 좀 더 예측 가능하게 된다.


## Redux
### 3가지 원칙
- Redux는 state를 위해 단 한개의 store를 사용한다.(Flux는 여러개의 store) (store의 데이터 구조는 javascript 객체)
- State는 읽기 전용이다.
  - state를 변경하기 위해서는 action이 dispatch(보내져야) 되어야 한다.(action은 어떤변화가 일어나야 할 지 알려주는 객체)
- 변화는 순수 함수로 만들어져야 한다.
  - 위에서 action객체를 처리하는 함수를 Reducer라고 한다.
  - action이 어떤 변화를 일어나야 할지 알려주는 객체라면, Reducer는 그 정보를 받고 애플리케이션의 상태를 어떻게 바꿀지 정의한다.
  - Reducer는 순수함수로만 작성되어야 한다
    - 외부 네트워크 혹은 데이터베이스에 접근하지 않아야한다.
    - return 값은 오직 parameter 값에만 의존해야 한다.
    - 인수는 변경되지 않아야한다.
    - 같은 인수로 실행된 함수는 언제나 같은 결과를 반환해야 한다.
    - 순수하지 않은 API 호출을 하지 말아야 한다.(Date, Math 함수 등)


