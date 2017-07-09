FDS-38-storage,HTML메서드,restAPI
========


## DOM 스토리지(DOMStorage)
- 참고: <https://developer.mozilla.org/ko/docs/Web/API/Storage>
- 참고: <http://ohgyun.com/417>
- WebStorage API

### storage
- 메모를 저장하고 난 후 브라우저를 새로고침해도 메모가 남아있게끔 하는 간단한 예제
- storage 기술을 활용(웹 브라우저 저장공간, 약 5MB)
- 저장할때는 문자로 
- 전역객체 종속되어있는 `window.localStorage`
- `setItem(key, value)`
- `getItem()`
- `removeItem()
```js
localStorage.setItem('temp',{name: 'hoon'}) // undefined
localStorage.getItem('temp')
localStorage.removeItem('temp')
```

1. localStorage 
- 반영구적으로 기억
- 도메인 서비스 제작자가 지우거나, 사용자가 지우거나

2. sessionStorage 
- 세션이 유지되는 동안 접근 가능, 세션이 만료되면 제거
```js
sessionStorage
```
3. JSON.parse() -> 문자를 객체화
4. JSON.stringify() -> 객체를 문자화

## this.classList.contains









## MVC (Model View Controller)
- 모델에 변화가 있으면 컨트롤러가 
- view는 프론트엔드

## HTTP통신의 메서드
- 4개를 다 정확하게 쓰는것이 resFUlAPI
- GET
  - 목적지 주소
  - body가 없다.
  - 쿠키, 인증(엡솔레인션?)
- POST
  - POST로 나머지를 할 수 있지만 경량화 하기 위해
- PUT
- DELETE



## hdb파일
- 핸들바


## 실습
- package.json 파일 만드는 명령어
```bash
$ npm init -y
```
- 전역에 json-server 설치
```bash
$ npm install --global json-server
```

## REST API
- 참고: <https://www.npmjs.com/package/json-server>
- 참고: <https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop/related?hl=en>
- 코딩을 하지 않아도 된다. -> 백엔드를 신경쓰지 않아도 된다.
- 네이티브 뷰 live-server
- json-server
- live-server
```bash
$ json-server DB/people.json

  \{^_^}/ hi!

  Loading DB/people.json
  Done

  Data must be an object. Found object.See https://github.com/typicode/json-server for example.
```


### GET
- 데이터를 가져오는데,
- key, value 가 일치하는 데이터를 가져온다.

## 메모앱
```bash
$ json-server --port 3004 DB/memo-app.json --watch
```