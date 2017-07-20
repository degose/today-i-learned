FDS-48-webpack,모던js
========

- 참고: <https://goo.gl/B0FxAR>
- 슬라이드: <http://slides.com/sohpaul/deck#/>
- 참고: <https://github.com/paulsoh/fastcampus_webpack_tutorial>

## 모던 js
- 이제 ES6도 최신이 아님 계속해서 개정되는 JavaScript

## 텀블벅 vs 와디즈 스크립트 비교
- 스크립트가 하나 있는 것과 여러개 있는 것

## webpack이란?
- 참고: <http://d2.naver.com/helloworld/0239818>
- CommonJS, AMD 참고: <http://d2.naver.com/helloworld/12864>
- 서버에서 처리하는 로직을 JavaScript로 구현하는 부분이 많아지면서 웹 서비스 개발에서 JavaScript로 작성하는 코드의 양도 늘어났다. 코드의 양이 많아지면 코드의 유지와 보수가 쉽도록 코드를 모듈로 나누어 관리하는 모듈 시스템이 필요해짐. 그러나 JavaScript는 언어 자체가 지원하는 모듈 시스템이 없기 때문에 이런 한계를 극복하려 여러 가지 도구를 활용하는데 그 도구 가운데 하나가 webpack
- webpack은 JavaScript 모듈화 명세를 만드는 대표적인 작업 그룹 CommonJS와 AMD의 명세를 모두 지원하는 JavaScript 모듈화 도구다.
- 장점
  - 다른 module bundler에 비해 performance가 우수하다.
  - Loader가 존재하여 다른 리소스를 순수 JavaScript로 변환하고 모든 리소스에 대한 모듈을 구성해 준다.
  - babel을 사용하여 ES6와 같이 브라우저에서 지원되지 않는 script code를 변환하여 사용할 수 있다.
  - 3rd-party library에 대해 모듈로 통합하는 기능을 제공한다.
  - module bundler의 대부분의 기능을 사용자가 커스터마이징하여 사용할 수 있다.
  - 다양한 플러그인을 제공한다.


## Adding Loaders
### Loader
- webpack의 로더는 다양한 리소스를 JavaScript에서 바로 사용할 수 있는 형태로 로딩하는 기능이다. 로더는 webpack의 특징적인 기능이면서 webpack을 강력한 도구로 만드는 기능이다.
### babel-loader
- webpack이 Babel을 이용하여 자바스크립트를 트랜스파일할 수 있도록 기능을 제공한다. 이 패키지는 내부적으로 몇 가지 핵심적인 Babel 패키지를 가지고 온다.
```bash
$ npm install --save-dev babel-loader babel-cli
```
### css-loader, style-loader
- css-loader, style-loader를 같이 써준다.
- Webpack은 모듈안에 의존적인 CSS파일들을 검색한다. webpack은 require(‘파일이름.css’)을 가지고 있는지 JS파일을 체크한다. 만약 찾았다면, 먼저 해당 파일을 css-loader 수행한다. css-loader는 모든 CSS와 그안에 의존적인 다른 CSS(ex: import otherCSS) 를 로드한다. 그후 Webpack은 결과들을 style-loader로 보낸다.
```bash
$ npm install --save-dev css-loader style-loader
```
- css파일들을 import해준다.
```js
import 'todomvc-common/base.css';
import 'todomvc-app-css/index.css';
```
### webpack.config.js 파일
```js
const resolve = require('path').resolve;

module.exports = (env) => ({
  context: resolve('js'),
  entry: "./routes.js",
  output: {
    path: resolve('dist'),
    filename: './bundle.js',
    publicPath: '/dist/',
    pathinfo: true,
  },
  module: {
    loaders: [
      {
        test: /\.js$/,
        loaders: ['babel-loader'],
        exclude: '/node_modules/',
      },
      {
        test: /\.css$/,
        loaders: ['style-loader', 'css-loader'],
      },
      {
        test: /\.(png|jpg|gif)$/,
        loader: 'url-loader',
        query: {
          limit: 1024,
          name: 'assets/[name].[hash:8].[ext]',
        }
      },
    ],
  },
  devtool: env.dev ? 'eval' : 'source-map',
})
```



## webpack Part.1
### Bundler의미와 필요성
- Bundle, Bundling, Bundler
- Webpack v2
- Gulp, Grunt
  - Gulp의 task 개념
  - webpack은 task

## 실습
- 참고: <http://todomvc.com/>
- 프레임워크들을 비교할 수 있다.

- http-server 설치
```bash
$ npm install --save-dev http-server
$ vi package.json
$ http-server
$ ./node_modules/.bin/http-server
```
- webpack 설치
```bash
$ npm install --save-dev webpack
# 출력파일 -> 새파일
$ ./node_modules/.bin/webpack js/routes.js abc.js
```
- require??

- watch 와 -p
- 배포 파일들은 ugly파일 -> 용량이 적고 어차피 읽을 필요가 없으니까
```bash
$ ./node_modules/.bin/webpack --watch js/routes.js abc.js
$ ./node_modules/.bin/webpack -p js/routes.js abc.js
```
- 더 좋은 환경
```bash
$ npm install --save-dev webpack-dev-server
$ ./node_modules/.bin/webpack-dev-server js/routes.js abc.js
```
- => 이걸로 알 수 있는 것 webpack으로 배포용, 개발용 따로 서버를 돌릴 수 있다.

- package.json에 scripts 파일 만들기
```js
"scripts": {
  "build": "webpack -p js/bundle.js abc.js",
  "build:dev": "webpack js/bundle.js abx.js",
  "dev": "webpack-dev-server js/bundle.js abc.js"
}
```
- 실행 명령어는 
```bash
$ npm run build(키워드)
```


- module.exports webpack이 쓰는 문법이다.
- 어떤 것을 exports 할 거냐. 객체에다가 key, value 값을 넣을 것
- webpack.config.js 파일 만들기
```js
module.exports = {
  entry: "./js/routes.js",
  output: {
    filename: "./bundle.js",
  },
}
```
- package.json 파일도 수정
```js
"scripts": {
  "build": "webpack -p",
  "build:dev": "webpack",
  "dev": "webpack-dev-server"
}
```


