FDS-54-추가강의1
========

## 참고 링크
- vue-cli: <https://github.com/vuejs-kr/vue-cli>
- vue-loader: <https://vue-loader.vuejs.org/kr/>
- vue-router: <https://router.vuejs.org/kr/>
- vuex: <https://vuex.vuejs.org/kr/>
- vue.js SSR(서버사이드렌더링): <https://ssr.vuejs.org/ko/>
- nuxt.js(vue node.js 프레임워크): <https://ko.nuxtjs.org/>

## 강의 수강 목록
### Vue Transition/Animation & JavaScript Hook
- ~~Vue CLI 를 활용하여 프로젝트 설정~~
- ~~단일 엘리먼트 전환 효과~~
- ~~슬라이드 전환 효과~~
- ~~바운스 효과 및 초기 로딩 시 애니메이션 적용 속성~~
- Animate.css 라이브러리 활용 방법
- 애니메이션 유형 동적 변경
- 엘리먼트 사이 전환 효과
- 컴포넌트 사이 전환 효과
- 리스트 트랜지션
- Lodash 라이브러리를 활용한 셔플 효과

### vue-resource + Google Firebase 활용 Ajax 비동기 통신
- ~~Vue Resource - 프로젝트 스케폴딩 (using Vue CLI)~~
- ~~Vue Resource - 파이어베이스 설정 (Firebase Setting)~~
- ~~Vue Resource - POST 메서드 통신으로 Firebase에 데이터 추가~~
- ~~Vue Resource - GET 메서드 통신으로 Firebase에서 데이터 로드~~
- ~~Vue Resource - 전역 환경설정 (Global settings)~~
- ~~Vue Resource - 인터셉터 (Interceptors)~~
- ~~Vue Resource - resource() 객체 커스텀 메서드 등록~~
- ~~Vue Resource - URI 템플릿 (Templates) 활용~~

### vue-router를 활용한 SPA 구현
- ~~Vue Router - 모듈 설치 및 라우팅 설정~~
- ~~Vue Router - 라우터 링크 컴포넌트~~
- ~~Vue Router - 동적 라우팅 처리~~
- ~~Vue Router - 중첩된 라우팅~~
- ~~Vue Router - 이름을 가지는 라우트 연결~~
- ~~Vue Router - 쿼리 파라미티 & 이름이 있는 라우터 뷰~~ <= 이거 다시
- ~~Vue Router - 리다이렉트 라우팅 (redirect routing)~~
- Vue Router - 트랜지션/애니메이션 라우팅
- Vue Router - 라우트 컴포넌트에 속성 전달
- Vue Router - 뒤로 가기 라우팅 go(-1)
- Vue Router - 스크롤 동작(scrollBehavior)
- Vue Router - 내비게이션 가드(Navigation Guard)
- Vue Router - 지연로딩(lazy loading)

### Vuex 상태 관리 패턴 라이브러리
- Vuex - 뷰엑스 컨셉(Concept)
- Vuex - 실습 자료 준비(Preparing, 무음)
- Vuex - 스테이트(State)
- Vuex - 게터(Getters)
- Vuex - 뮤테이션(Mutations)
- Vuex - 액션(Actions)
- Vuex - 엄격 모드(strict mode)
- Vuex - 엄격 모드에서의 폼 핸들링(strict mode form handling)
- Vuex - 모듈(Modules)
- Vuex - 모듈 네임스페이스(Modules Namespace)

## vue-cli 사용법
- 스캐폴딩 준비
```bash
$ vue init webpack-simple [파일이름]
$ npm install
```

## vue-resource
- 참고: <https://github.com/pagekit/vue-resource>
- 서버랑 통신하기 위한 http를 ajax로 처리해주는 객체
```bash
$ npm i vue-resource
```
```js
import VueResource from 'vue-resource';
Vue.use(VueResource);
```
### firebase설정
- 프로젝트 추가
- Database
- rules
  - 외부에서도 접근 가능하게 'true'로 변경
  ```js
  {
    "rules": {
      ".read": "true",
      ".write": "true"
    }
  }
  ```
### App.vue 에서 firebase 데이터 저장, 불러오기
- input에 텍스트를 쓰고 submit하면 firebase 데이터 안에 해당 텍스트가 더해진다.
```pug
<template lang="pug">
  #app
    div.post-http
      input(type="text" v-model="user_input.task")
      button(type="button" @click="submitData") Submit

    div.get-http
      button(type="button" @click="fetchData") Fetch

    ul.fetched-data
      li.fetched-data-item(v-for="data in datalist")
        label
          input(type="checkbox" v-model="data.done") 
          | {{ data.task }}
</template>
```
```js
<script>
export default {
  name: 'app',
  data () {
    return {
      user_input: {
        done: false,
        task: ''
      },
      datalist: []
    }
  },
  methods: {
    submitData(){
      // VueResource === this.$http
      // firebase에서 copy한 주소
      // Axios와 비슷
      this.$http.post('https://vue-http-5033e.firebaseio.com/todoList.json', this.user_input)
                .then(response => console.log(response))
                .catch(error => console.log(error.message));
    },
    fetchData(){
      this.$http.get('https://vue-http-5033e.firebaseio.com/todoList.json')
                .then(response => {
                  return response.json();
                })
                .then(data => {
                  this.datalist = Object.values(data);
                })
                .catch(error => console.log(error.message));
    }
  }
}
</script>
```

## Vue Router
- 설치
```bash
$ npm i -D vue-router
```
```js
import VueRouter from 'vue-router';
Vue.use(VueRouter)
```



