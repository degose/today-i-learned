FDS-52-form
========


### Vue 폼 유효성 검사
- input , textarea, select ... => v-model
- Modifiers: .lazy, .number, .trim
- multi: checkbox, multiple ... []

### Vue 컴포넌트 (중첩)
- Define Global Component: Vue.component(id, {})
- SET: Vue.component(id,{}) === function(constructor, class)
- GET: Vue.component(id)
- ParentComponent: `<slot>`
- ChildComponent: `<slot>`
```html
<parent>
  <child>Child component</child>
</parent>
```
- .is

## 통신
- 부모와 자식
- 가능한한 분리된 상태로 유지하는것이 중요하다.
- 각자 캡슐화 해서 관리가 용이하다.(iife 패턴과 유사)
- 부모 => [props] => 자식
- 부모 <= [event] <= 자식
- 부모는 자식에게 데이터를 전달
- 자식은 자신에게 일어난 일을 부모에게 알린다.

### props 전달하기
- 모든 컴포넌트 인스턴스에는 자체 격리 된 범위가 있다.
- 자식에게 props 옵션을 사용

### props 속성 바인딩
- v-bind
- : 있고 없고에 따라 문자열로 전달 or 숫자로 전달 다르게 된다.
- 단방향 데이터 흐름
- 하위 컴포넌트가 실수로 상위 컴포넌트를 수정하는 것을 막을 수 있다.
- 이 prop는 초기 값을 전달 하는데만 사용하자.
- prop는 변경되어야 할 원시 값으로 전달된다. (바로 복사해서 사용가능)
- 부모에서 전달된 속성 유형이 참조형이라면
- 객체, 배열이라면... 자식은 그 데이터를 그대로 사용하여 수정하면 안된다.
- 만약 자식이 부모의 속성값을 바꾸고 싶다면, 
  - 방법 1. 속성값을 복사해서 바꿔야 한다.(로컬 데이터 속성으로 사용)
  - 방법 2. 부모에게 수정 요청을 한다. (이벤트 발신)

### 검증
- 반드시 전달, 타입은 문자만 가능
  - type
  - required
- 참조형 데이터의 경우, 함수를 통해 객체를 반환해야 한다.
```js
propMessage: {
  type: Array,
  default: function(){
    return ['오늘도'];
  }
}
```
- 참고: <https://kr.vuejs.org/v2/guide/components.html#Props로-데이터-전달하기>

## Custom Event(사용자 정의 이벤트)
- $on(evemt) <---- $emit(event)
- jQuery().on()과 유사 <---- jQuery().trigger() 과 유사
- addEventListener와 dispatchEvent와는 다르다.

## Event Bus
- 부모 자식간의 중첩이 많아지면 관리가 어려워짐
- 부모와 자식간의 관계가 아닌 구조에서 이벤트 수신
- 글로벌 이벤트 버스
- 공통의 데이터 관리가 가능하다.
```js
var bus = new Vue
bus.$emit('id-selected',1)
bus.$on('is-selected', function(id){})
```
- EventBus {} 생성
- 이벤트 수신 .$on(id, callback)
- 이벤트 수신 제거 .$off()
- 1회 이벤트 수신 .$once()
- 이벤트 발신 .$emit(id,payload)

## 이벤트 1회 수신(Once)

## 슬롯
- 이름을 가지는 슬롯
```html
<header>
  <slot name="header"></slot>
</header>
```
- 범위를 가지는 슬롯

## scope
## 