수FDS-34-속성제어,이벤트,객체지향
========


## UI-TAB 실습

## 속성 제어
- `.hasAttribute()`
- `.getAttribute()`
- `.setAttribute()`
- `.removeAttribute()`
### utils 함수 만들기
- FDS.attr(prop)       : GET
- FDS.attr(prop, value): SET
- FDS.removeAttr(prop) : DELETE
```js
// FDS.attr(el | nodelist, prop, value)
// get set value가 있고 없고 구분
// o를 each문 돌리기 위해서 노드 리스트
var attr = function (o, prop, value) {
  if ( !o || !prop ) {
    throw '첫번째, 두번째 전달인자는 필수입니다';
  }
  // o는 존재하고,
  // o는 요소노드인가? (Element Node)
  // o는 유사배열인가? Nodelist, HTMLCollection 인가?
  if ( o && o.nodeType === 1 ) {
    o = [o];
  }
  // GET(가져온다)
  if ( !value ) {
    return o[0].getAttribute(prop);
  }
  // SET(설정한다)
  else {
    each(o, function (item, index) {
      item.setAttribute(prop, value);
    });
  }
};
```
- 응용
```js
(function(global, $){
  'use strict';

  var container = $.selector('.container');
  var container_lis = $.selectorAll('li', container);

  // SET
  $.attr(container_lis, 'style', 'color: tan');
  // GET
  console.log( $.attr(container_lis, 'style'));

})(window, window.FDS);
```
## 스타일 제어
- `.style`
- `.cssText`
- `.getComputedStyle | currentStyle`
- 예전에는 인라인 스타일들을 개발단에서 넣으면서 레이아웃이 무너지는 일이 발생한다. 왜 인라인으로 스타일을 줬을까 -> 인라인 스타일을 설정하면 .style 로 가져올 수 있었다.
1. MS IE 8-
`list.currentStyle.fontSize`
2. W3C Standard
`window.getComputedStyle(list).fontSize // 16px`

- 과제 [css utils 함수 만들기]
FDS.css(list, 'font-size', '+=32px')
이렇게 할 수 있게
$.css(list, '\
  font-size: 200px;\
  padding: 100px;\
  margin: 20px;\
);

## 리페인팅 리플로우
- 참고: <https://goo.gl/NxU2Qn>
- 참고: <http://cwdoh.com/workshop/2014/06/14/understanding-rendering-performance-matters-in-chrome/>
- 참고: <http://untitledtblog.tistory.com/45>
- 트렌지션 트렌스폼 이용

## first-class citizen 복습
- 참고: <http://changsuk.me/?p=1916>
- 프로그래밍 언어의 설계 시에 런타임에 프로그램 흐름의 중심으로 결정한 엔터티
- 프로그램이 실행되면 객체들 간의 관계(어떤 객체가 어떤 객체를 참조하는지, 메소드는 어떤 객체를 인수로 받아서 어떤 객체를 반환하는지)에 의해 프로그램의 행태가 결정된다. 
  - 변수와 자료구조에 저장될 수 있다.
  - 하위 루틴의 파라미터로써 전달될 수 있다.
  - 하위 루틴의 수행 결과로써 반환될 수 있다.
  - 런타임에 구성될 수 있다.
  - 어떤 명칭(예, 변수명)이 부여되는지에 상관 없이, 독립적이고 고유한 엔터티다.


## 함수지향, 객체지향
- 참고: <https://goo.gl/BfgOx3>
- first-class citizen이 함수 그 자체 -> 함수지향
- first-class citizen이 객체 or 클래스 -> 객체지향

### 함수지향
- 데이터 -> 함수(절차) -> 결과 -> 함수(절차) -> 결과

### 객체지향 프로그래밍 (OOP)
- 참고: <http://vandbt.tistory.com/m/39>
- Object-Oriented Programs
- 캡슐화, 다형성, 상속 을 이용하여 코드 재사용을 증가시키고, 유지보수를 감소시키는 장점을 얻기 위해서 객체들을 연결 시켜 프로그래밍 하는 것
1. 객체(Objects)
  - 데이터 : 객체의 상태를 기술하는 정보를 저장. 객체는 데이터를 가지고있는 작은 프로그램처럼 동작한다.
  - 행위의 집합 : 객체에게 작업을 수행하도록 요청하는 것을 '메세지를 보낸다'라고 함. 이 메세지를 받았을 때 객체가 어떻개 해야하는지 알고 있는 것
  - 아이덴티티 : 어떠한 객체를 다른 객체와 구분하는 유일한 아이덴티티를 가진다. 이것은 구조적 언어의 변수와 닮았다.
2. 클래스(Classes)
  - 클래스와 객체의 구분
  - 클래스는 객체가 소유하게 될 속성 attributes 과 행위 behaviors 를 정의
  - 객체가 이해할 수 있는 메세지와 메세지에 응답하는 과정을 정의 
  - 각각의 메세지에 대해 메소드 method 라고 불리우는 프로시저를 만들고, 이것을 구현
3. 캡슐화(Encapsulation)
  - 구현으로 부터 인터페이스를 분리하는 것
  - 객체는 속성과 메소드로 이루어져있다.
  - 인터페이스 interface : 속성과 메소드를 객체의 외부에서 접근 하는 것 (자동차의 핸들, 가속 페달, 브레이크 - 간단, 규격화)
  - 구현 implement : 속성, 메소드를 객체 자신만의 사적인 용도로 예약한 것 (자동차의 내부 점화, 실린더, 연료 분사 - 유동적)
4. 상속(Inheritance) 
  - 상속의 진가는 강력한 추상 구조화 이다.
  - 새로운 종류의 서브클래스를 작성하면, 부모 super class 에 이미 내장된 기능들을 사용할 수 있다.
  - 상속을 사용하면 공통적인 요소를 슈퍼클래스에 정의 함으로써 일반화 할 수 있다. 
5. 다형성(Polymorphism)
  - 캡슐화, 상속과 함께 작동해서 객체-지향 프로그램의 흐름 제어 flow of control 를 단순화 한다.
  - 상속 계층의 연관된 객체에 메세지를 보냄으로써 단순화
  - ISA 관계 : 클래스 A가 클래스 B의 서브클래스 라면, A 객체는 B객체가 할 수 있는 모든 일을 할 수 있다. A객체는 B객체라고 말할 수 있고, 이런 경우의 상속 관계
  - 다형성으로 조건문을 제거하라. 동작이 그 타입에 따라 변하는 객체를 가지고 있을 때, 명시적으로 조건문을 사용하지 않아도 되도록 한다.
- 장점
  - 신뢰성 있는 소프트웨어를 쉽게 작성할 수 있다. (개발자가 만든 데이터를 사용하기에 신뢰할 수 있다.)
  - 코드를 재사용하기 쉽다.
  - 업그레이드가 쉽다.
  - 디버깅이 쉽다.
- 단점
  - 하나의 기능을 불러오려면 모듈 전체를 가져와야 하기 때문에 프로그램 사이즈가 더 커질 수도 있다.
  - 메소드를 통해서만 접근이 가능하기 때문에 딱 찍어서 접근할 수 없고, 경로를 통해서만 접근이 가능해 속도적인 측면에서 불이익이 있습니다.


## 이벤트 걸기
- W3C 표준 모델 : addEventListener 
- MS 비표준 모델 : attachEvent
- 구형 이벤트 모델 : on{type}

- Cross Browsing Event Utility Function
```js
function addEvent(el, type, handler, capture) {
  if ( el.addEventListener ) {
    capture = capture || false;
    el.addEventListener(type, handler, capture);
  } else if ( el.attachEvent ) {
    el.attachEvent('on'+type, handler);
  } else {
    el['on'+type] = handler;
  }
}
```
## 이벤트 삭제
- .removeEventListener() | .detachEvent()
- 함수 값이 아닌, 참조 변수를 설정해야만 제거가 된다.
```js
global.addEvent = function(){
  var _addEvent = null;
  if ( 'addEventListener' in EventTarget.prototype ) {
    _addEvent = function(el, type, handler, capture) {
      el.addEventListener(type, handler, capture || false);
    };
  } else if ( 'attachEvent' in EventTarget.prototype ) {
    _addEvent = function(el, type, handler, capture) {
      el.attachEvent('on'+type, handler);
    };
  } else {
    _addEvent = function(el, type, handler, capture) {
      el['on'+type] = handler;
    };
  }
  return _addEvent;
}();
global.removeEvent = function(){
  var _removeEvent = null;
  if ( 'removeEventListener' in EventTarget.prototype ) {
    _removeEvent = function(el, type, handler, capture) {
      el.removeEventListener(type, handler, capture || false);
    };
  } else if ( 'attachEvent' in EventTarget.prototype ) {
    _removeEvent = function(el, type, handler, capture) {
      el.detachEvent('on'+type, handler);
    };
  } else {
    _removeEvent = null;
  }
  return _removeEvent;
}();
```
## 이벤트 기본 동작 차단
- e.preventDefault()
- return false

## 이벤트 전파
### 이벤트 버블링, 캡쳐링
- 드래그엔 드롭할 때 여러개의 이벤트가 중첩되면서 발생
- 이벤트 버블링(Bubbling) : 최상위 엘리먼트에서 대상 엘리먼트까지 이벤트가 전파되는 것
- 이벤트 캡쳐링(Capturing) : 이벤트 대상 엘리먼트를 시작으로 최하위 엘리먼트까지 이벤트가 전파가 되는 것
- 자식 엘리먼트에 클릭 이벤트가 발생하여 최상위(또는 최하위) 엘리먼트까지 이벤트가 전파될 때, 이벤트 리스너(콜백 함수)의 인자를 통해 이벤트 대상 엘리먼트를 가져올 수 있는데, 그게 바로 target과 currentTarget이다.
- event {} target 은 이벤트가 진행 중인 자식요소
- event {} currentTarget 은 이벤트가 연결된 부모요소

### 이벤트 버블링 차단
- 프로파간다
- stoppropagation
- 즉시 중단하라 (해당되는 하나의 이벤트만 실행하고 나머지는 멈춰라)
stopimmediatePropagin
- 캡쳐링인지 버블링인지에 따라 달라진다.
  // 전파 차단
  // e.stopPropagation()
  // e.stopImmediatePropagation()

라이브러리 객체로 설정하는 법을 터득하면 D3 데이터 시각화 문법과 똑같기 때문에 좋다.





## 주요 이벤트

### 스크롤 이벤트
- 스크롤 내릴때마다 애니메이션 생기는 페이지들
- 애플 사이트 GOOD
- 블리자드 채용 페이지 때 백뭐시기 필터 참고
- offsettop
- scrollY - top에서부터의 거리 숫자값이 나온다.

### 키보드 이벤트
키 다운
- onkeydown
키 프레스
- onkeypress
키 업
- onkeyup

### 마우스 이벤트
클릭
- onclick

마우스 오버
- onmouseover
마우스 아웃
- 
마우스 엔터
- 
마우스 리브
- 
마우스 무브
마우스 업
마우스 다운

더블클릭
- ondbclick
- 하나의 이벤트에 클릭과 더블클릭을 함께 사용하는 것은 안된다.


### 폼이벤트
서브밋
리셋
- 입력값  ㅇ초기화
체인지
- 


## 이벤트 타겟
## 이벤트 객체
## 이벤트 관계요소

```js
// document.onclick = function(e) {
//   e = e || window.event;
//   e.target = e.target || e.srcElement;
//   e.relatedTarget = e.type === 'mousever' ? e.fromElement : e.toElement;
// };

var actionA = function() {
  console.log(this, 'actionA');
};
var actionB = function() {
  console.log(this, 'actionB');
};

addEvent(list, 'click', actionA);
addEvent(list, 'click', actionB);
addEvent(list, 'click', function(){
  removeEvent(this, 'click', actionB);
});
```


## oojs-Store.js
- 스토어(저장소) 데이터 관리 패턴을 적용한 라이브러리
- Store 생성자 함수
```js
var book_list = new Store();
var music_collection = new Store();
var travel_history = new Store();
```
- Store 객체를 사용해서 할 수 있는 일
- CRUD 기능
  - 추가 Create
  - 읽기 Read
  - 쓰기(수정) Update
  - 제거 Delete
  - 소유(검증) has

- Store API
- [private]
  - state

- [public]
  - .pushData(data)
  - .readData([index])
  - .writeData(index, fixed_data)
  - .removeData([index])

```js
// 생성 패턴 (Creation Pattern)
// 생성자(Constructor) + 프로토타입(Protype) 패턴 사용
var Store = (function(global){
  'use strict';
  // 비공개 저장소
  var state = [];
  // 생성자 함수
  function Store(data) {
    this.init(data);
  }
  // 프로토타입 (공용 속성/메서드)
  Store.fn = Store.prototype;
  Store.fn.init = function(data) {
    if ( Array.isArray(data) ) {
      state = data;
    }
  };
  Store.fn.hasData = function(index) {
    return !!state[index];
  };
  Store.fn.readData = function(index) {
    if ( index === undefined ) {
      return state;
    } else if ( typeof index === 'number' && index >= 0 ) {
      return state[index];
    } else {
      throw '0 이상의 숫자 값을 전달하거나, 아무런 값을 입력하지 않아야 합니다.';
    }
  };
  Store.fn.pushData = function(item){
    item && state.push(item);
  };
  Store.fn.writeData = function(index, new_item){
    if ( index && new_item && this.hasData(index) ) {
      state.splice(index, 1, new_item);
    }
  };
  Store.fn.removeData = function(index){
    if ( index && this.hasData(index) ) {
      state.splice(index, 1);
    }
  };
  return Store;
})(window);
```
- 싱글톤(Singleton) 객체
```js
var store = {
  state: [],
  readData: function() {},
  writeData: function() {},
  pushData: function() {},
  removeData: function() {}
};
```

