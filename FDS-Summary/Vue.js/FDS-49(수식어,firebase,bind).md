FDS-49-수식어,firebase,bind
========

## modifier
### 이벤트 수식어
  - stop: 이벤트 전파 차단
  - prevent: 기본 동작 차단
  - capture: 이벤트 캡쳐링 사용
  - self: 이벤트 타깃이 자신일 경우에만 이벤트 적용 (자식 엘리먼트에서는 안된다.)
  - once: 1회 이벤트 바인딩
- 체이닝이 가능하다.
- 단순히 수식어만 사용 가능
```html
<form v-on:submit.prevent></form>
```
- 예시: a태그의 기본동작 차단을 하고싶은 경우
```pug
//- button.is-small.delete(type="button" aria-label="제거")(v-on:click="excludeMember(i,n)")
a.is-small.delete(href="" role="button" aria-label="제거")(@click.prevent.stop="excludeMember(i,n)")
```

### key 수식어
  - enter
  - tab
  - delete == backspace
  - esc
  - space
  - up
  - down
  - left
  - right
  - ctrl
  - alt
  - shift
  - meta(command mac,window 달라서)
```html
<input v-on:keup:enter="update">
```

### 사용자 정의 key 수식어 설정
- shift + f2를 누르고 싶은데 f1,f2는 수식어로 등록되어 있지 않다.
- 등록
```js
Vue.config.keyCode.f1 = 112;
Vue.config.keyCode.f2 = 113;

// 다수의 key등록 시 이렇게도 가능
Vue.config.keyCodes = {
  f1: 112,
  f2: 113
};
```
- 사용
```pug
button.delete(type="button" aria-label="제거" @keyup.shift.f2="excludeMember(i,n)")
```




## argument

## 왜 겸손한 자바스크립트를 안하나?
- 모든 뷰 핸들러 함수와 표현식 샌드박스 패턴으로 엄격히 관리하기 때문에 유지보수가 어렵지 않다.
- 직접 수동으로 요소를 찾아서 하지 않아도 직관적으로 줄 수 있다.
- viewModel이 파기되면 모든 이벤트 리스너가 자동으로 제거, 이벤트 제거에 대한 걱정이 필요 없어진다.



## firebase
- 참고: <https://firebase.google.com/>

## prop
- 속성 대신 DOM속성으로 바인딩 (property 대신 attribute로 바인딩)

## attr