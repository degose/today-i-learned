# 생활코딩 Node.js & Express - module

## 코드 설명
```js
const http = require('http');
// http 라는 상수에 http 모듈을 담은 것

const hostname = '127.0.0.1';
const port = 3000;

// http.Server라는 새로운 객체를 얻는다. -> 그 객체는 listen이라는 메소드를 가지고 있기 때문에 그것을 호출할 수 있다.(객체지향 ㅎㅎ)
const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

## OS 모듈 써보기
- module.js
```js
const o = require('os');
console.log(o.platform());
```
- bash
```bash
$ node module.js
darwin
```

## NPM(Node Package Manager)
- HTTP, OS => Nodejs가 제공하는 모듈
- Date, String, Array => JavaScript가 제공하는 모듈
- Node 계의 앱스토어
- 설치 / 삭제 / 업그레이드 / 의존성 관리
- 링크 : https://www.npmjs.com/

### 독립적 소프트웨어 설치해보기
- pretty.js
```js
function hello(name) {
  console.log('Hi,'+name);
}
hello('gose');
```
- uglify 프로그램을 설치, 실행
```bash
$ npm install uglify-js -g
$ uglifyjs pretty.js
# 빈 공백을 없애서 한 줄로 만들어 준다.
function hello(name){console.log("Hi,"+name)}hello("gose");
$ uglifyjs pretty.js -m
# 불필요한 인자 값도 짧은 문자로 대체
function hello(o){console.log("Hi,"+o)}hello("gose");
$ uglifyjs pretty.js -o uglified.min.js -m
# 다른 이름으로 저장
```

### 모듈 설치해보기
- 패키지 설정하기 -> package.json 파일 생성
```bash
$ npm init
package name: (nodejs)
version: (1.0.0)
description: server side javascript tutorials
entry point: (hello.js)
test command:
git repository:
keywords:
author:
license: (ISC)
About to write to /Users/gose/study/NodeJs/package.json:

{
  "name": "nodejs",
  "version": "1.0.0",
  "description": "server side javascript tutorials",
  "main": "hello.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}


Is this ok? (yes) yes
```
- underscore 설치
- 링크: http://underscorejs.org/
```bash
$ npm install underscore
$ npm install underscore --save
# package.json 안에 dependencies 안에 들어가서 의존성을 갖고 있는 패키지의 기능을 제공
```
- package.json
```json
"dependencies": {
  "underscore": "^1.8.3"
}
```
- underscore.js
```js
// node_modules 안에 underscore 객체를 가져온다.
const _ = require('underscore');
const arr = [3,6,9,1,12];
console.log(arr[0]);
console.log(arr[arr.length-1]);
console.log(_.first(arr));
console.log(_.last(arr));
```
```bash
$ node underscore.js
3
12
3
12
```