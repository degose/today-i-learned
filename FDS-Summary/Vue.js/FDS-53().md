FDS-53-종강,
========


## 이미지 쓸 때
```pug
<template lang="pug">
  #app
    img(:src="./assets/logo.png", :alt="vue.label")

    //- 직접 에셋 속성을 설정하는 경우, assets/ 디렉토리에서 찾아야 이미지 출력
    //- file-loader를 통해 아래와 같이 처리되기 때문
    //- /dist/logo.png?82b9c7a5a3f405032b1db71a25f67021
    //- img(src="./assets/logo.png", :alt="vue.label")
</template>
```

## `<component :is="">`

## `<keep-alive>`
- 전환된 컴포넌트를 메모리에 유지. 상태보존. 다시 렌더링하지 않도록 
- `include` : 일치하는 컴포넌트 캐시
- `exclude` : 일치하는 컴포넌트 캐시되지 않는다.
- `<activated>`

## 재사용이 가능한 컴포넌트

## 요소노드 참조
- 때로 DOM제어를 해야할 일이 있다.
- 대상 찾기
- 밑줄이나 카멜표기법 쓰자
- `v-for`와 함께 쓰면 배열이 반환
- 컴포넌트가 렌더링 된 후에만 채워지며 반응적이지 않다.
- watch or 라이프사이클 훅(mounted)와 함께 쓰자
- `$refs`
```html
<div id="parent">
  <user-profile ref="profile"></user-propfile>
</div>
```
```js
var child = this.$refs.profile.alt;
```
```js
  mounted () {
  // DOM 스크립트 스타일
  let app = this.$el;
  this.logo_alternate_text = app.querySelector('img').getAttribute('alt');

  // Vue
  this.logo_alternate_text = this.$refs.logo_img.alt; // HTML_DOM
  this.logo_src = this.$refs.logo_img.src; // HTML_DOM

  // jQuery 스타일
  this.logo_src = $(this.$refs.logo_img).attr('src');

  console.log('this',this.$refs);

  },
```

## filter
- 필터는 체이닝이 가능하다.
- `|` 파이프를 사용
- main.js에서 전역에 등록하는 방법
```js
// 글로벌 Vue 필터 정의
Vue.filter('uppercase', v=> v.toString().toUpperCase());
Vue.filter('lowercase', v=> v.toString().toLowerCase());
```
- App.vue 에 등록하는 방법
```js
export default {
  name: 'app',
  filters: {
    currency: (value,sign="원") => {
      if(sign !== '원'){ return sign + value;}
      else {return value + sign;}
    }
  }
}
```
- 적용
```pug
p 특가 {{ 300 | currency }} 
//- 특가 300원
p 특가 {{ 300 | currency('$') }}
//- 특가 $300
```
### 실습 (세자리 숫자마다 콤마(,)넣는 filter 만들기
- 숫자(문자) => 문자화
- 1000
- 1000 + ''
- String(1000)
- (1000).toString()
- 문자 => 배열화
- '1000/
- ['1','0','0','0']
- 배열의 원소를 Reverse
- ['1','0','0','0'].reverse()
- 0001
- for문을 사용하여 각 원소를 순환한다.
- 3자리 마다 콤마(,)를 추가 삽입
- 000,1
- 배열을 reverse() 한 후, join()합니다.
- 1,000
- 문자 값을 반환

```js
Vue.filter('number', v=> {
  v = v.toString().split('').reverse();
  for(let i=0, vl=v.length; i < vl; i+=3) {
    i > 0 && v.splice(i, 1, v[i]+',');
  }
  return v.reverse().join('');
})
```
```pug
p 특가 {{ 12345300 | number | currency }}
//- 특가 12,345,300원
```

## vue2Filters
- 참고: <https://github.com/freearhey/vue2-filters>
- 설치
```bash
$ npm install vue2-filters --dev
```
- main.js에 불러오기
```js
import Vue2Filters from 'vue2-filters';

// Vue v2 Filters 플러그인 사용
Vue.use(Vue2Filters);
```

## directive
- 훅 함수
  - bind, inserted, update, component Update, unbind(v-if)
```pug
p 오늘은 
  a(href="" v-focus) 마지막 수업날
```
```js
directives: {
  focus: {
    inserted(el){
      el.focus();
    }
  }
}
```
- 전역 등록
```js
Vue.directive('focus',{
  bind(el,binding){
    console.log(binding.name);
    console.log(binding.args);
    console.log(binding.modifiers);
    el.focus();
  }
});
```

## Mixins
- 객체 합성 시스템
- 사용자 정의 옵션 처리 로직 주입에 활용
```js
let todoList_mixin = {
  created () {
    console.log('todoList Mixin Success!');
  },
  data() {
    input: ''
  },
  props: [],
  methods: {
    addTodoItem(){
      this.todos.push({
        content: this.inpul,
        complate: false
      })
    }
  }
}
```
```js
let MyComp = Vue.extend({
  mixons: [todoList_mixin]
})
```

## plugins
```js
Vue.use(MyPlugin)
MyPlugin.install = function(){}
```
- 참고: <https://madewithvuejs.com/>
- 참고: <http://vuematerial.io/#/>


## transition
- CSS 전환/애니메이션 상태 제어를 위한 class 속성(자동변환)
- Animate.css와 같은 타사 CSS 애니메이션 라이브러리 통합
- 전환 훅 중에 JavaScript를 사용하여 DOM을 직접 조작
- JavaScript 애니메이션 라이브러리와 통합하여 활용
- IE 10+
- 진입 `enter-class`
- 진행중
- 종료
```pug
<transition(name="animationType")></transition>
```

## animate.css
- 참고: <https://daneden.github.io/animate.css/>
```pug
transition(
  name=""
  enter-class="animated flipInX"
  enter-active-class=""
  enter=""
  enter=""
  enter=""
)
```

## SPA
### vue-router
- router 생성자 함수
```js
import VueRouter form 'vue-router';
global.router = VueRouter;
Vue.use(vueRouter)
```
- router.js
```js
import Vue from 'vue';
import VueRouter from 'vue-router';

Vue.use(VueRouter);

const routes = [
  {path: '/', component: require('./components/Home')}
  {path: '/fds', component: require('./components/FDS', children: [
    {path: 'profile', component: require('./components/FDS/profile'}
  ])}
  {path: '*', redirect('404')}
]
const router = new VueRouter({
  mode: 'history',
  routes
})

new router({

})
```
```pug
#app
  ul
    li
      router-link(to="/") HOME
    li
      router-link(to="/fds") FDS Home
```
### vuex
- 뷰 컴포넌트 간의 상태 공유(부모 자식 간)
- 상태관리 시스템
- 설치 후 store 저장소를 만든다.
```js
import Vue form 'vue';
import Vuex form 'vuex';

Vue.use(Vuex);

const store = new Vuex.Store({
  state: {},
  getters: {},
  mutations: {},
  actions: {}
})

export default store
```
```js
import store from './component/store'

openModal(){
  this.$store.commit()
}
```

