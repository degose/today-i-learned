FDS-46-vue.js 시작
========

- 설치 : <https://github.com/yamoo9/vue-project-template>
- vue 키노트 : <https://goo.gl/jZjQSY>


## 라우팅의 개념

## SPA 라우팅


## 특징
### vue-router
- component
- problem -> vuex

## vuex
- 데이터 관리
- 상태관리 매니저
- store 역할

## JSX

## server side rendering
- 접근성과 검색엔진 최적화를 위해서

## MVVM 아키텍쳐
- Model -> View Vodel -> View
## Expressions


## vanilla js vs jQuery Library vs Vue.js Framework

```js
Object.defineProperty(user, 'nickname', {
  get: function() { return nn; },
  set: function(v) { console.log('set event detection')}
})
```

## Vue.js vs Angular vs React
### Vue.js
- 독립 컴포넌트
- 디렉티브 -> DOM 제어에 집중
```js
Vue.directive('my-directive', {
  bind : function() {...},
  update : function() {...},
  unbind : function() {...}
})
```
- 필터
```js
Vue.
```




### Angular
- 그룹 모듈
- 디렉티브 -> 컴포넌트와 유사
```js
myModule.directive()
```
- 필터

### Vue.js
- Virtual DOM 감춰짐
- ES5


### React
- Virtual DOM 사용
- ES6
- JSX
- this.state.message

## Virtual DOM
- 가상 문서객체델
## Actual DOM
- 실제 문서객체모델


## 실습 (가상 하이퍼스크립트를 사용하여 VTree 만들기)
### budo

```bash
$ echo {} > package.json
$ npm i -D budo virtual-dom
$ touch package.json
```
- budo 설치
- <https://www.npmjs.com/package/budo>
```bash
$ npm run budo
```