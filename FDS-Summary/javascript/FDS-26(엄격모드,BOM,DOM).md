FDS-26-엄격모드, BOM, DOM
========

## 엄격모드(Strict)
- 오류 발생 가능성이 있는 코드를 제거하는 역할을 한다.
- 엄격 모드를 지원하는 브라우저에서는 오류 발생 가능성이 있는 코드 작성 시 오류를 발생하지만, 지원하지 않는 구형 브라우저는 이를 단순하게 무시한다. 즉, 호환성에 문제는 없다.
- 엄격 모드는 개별적인 유효범위(함수, 전역 유효범위 등)
```js
(function(global){
  'use strict'; // 엄격모드

  // gose = 'gose';        // [X]
  global.gose = 'gose';    // [O]

})(window);
```

### JavaScript 파일 병합(combine, merge) 시 주의
- IIFE 패턴은 문제를 일으킬 소지가 있다.
- 마지막에 ;(세미콜론)을 넣지 않아도 실행은 되지만 병합시 아래 코드와 한 줄로 병합되면서 문제를 일으킨다.
- 그러므로 함수코드 앞에 ;세미콜론을 넣어줘서 오류를 방지한다.(;;)세미콜론은 여러번 들어가도 오류를 발생시키지 않는다.
```js
(function(global){
  // dom-helper.js
  'use strict';
  // ....
})(window) // 이렇게 마지막에 ;(세미콜론)을 넣지 않는 경우

// 앞에 세미콜론을 넣어준다.
;(function(global){ 
  // dom-framework.js
  'use strict';
  // ....
})(window);
```

### 생성자 함수(Constructor Function)
- 생성자 함수.prototype ====> {}

### 네임스페이스 객체 선언
```js
var fds = function(){
  // 엄격모드 발동
  'use strict';

  // 사용자 정의 객체(UI 컴포넌트) 생성자 함수
  var Slider = function(min, max, value, step){
    'use strict';
    // new 키워드 없이 생성자 함수를 사용하면
    // this는 의도치 않은 객체를 가리켜 프로그램을 고장낸다.

    // new를 강제화 하는 패턴
    if ( this.constructor !== Slider ) {
      return new Slider(min, max, value, step);
    }

    // console.log('this ------', this);

    this.min = min || 0;
    this.max = max || 100;
    this.value = value || 0;
    this.step = step || 1;
  };

  Slider.prototype = {
    constructor: Slider,
    move: function() {},
    stop: function() {}
  };
  // 노출 패턴
  return  {
    // UI 카테고리
    ui: {
      Slider: Slider
    }
  };

}();


// 생성자 함수
function Fan(name) {
  // 'use strict';
  // 엄격 모드를 사용하면 this는 명시적으로 함수를 실행한 대상이 없어
  // undefined 이다. (검증)
  console.log(this);
  this.name = name;
}

// 엄격 모드를 사용하지 않을 경우
new Fan(); // this === Fan {}
Fan();     // this === window {}

// 엄격 모드를 사용할 경우
new Fan(); // this === Fan {}
Fan();     // this === undefined (명시적으로 실행하지 않아서)
```

## 일급객체
- Javascript 함수는 일반 함수로서 때론 생성자 함수, 함수의 인자, 함수의 반환 값(클로저), 객체의 멤버(메서드), 배열의 원소로서 다양하게 사용된다.

### 특징
- 변수, 데이터 구조 안에 담을 수 있다.
- 인자(Parameter, Argument)로 전달할 수 있다.
- 반환 값(Return Value)으로 사용할 수 있다.
- 런타임(실행) 중에 생성할 수 있다.
- 할당에 사용된 이름과 관계 없이 고유하게 식별할 수 있다.

```js
// CASE 1. 변수에 함수를 할당할 수 있다.
var showMeTheMoney = function(){};
// CASE 2. 함수의 인자로 함수가 전달될 수 있다.
function lifeCycle(callback) {
  typeof callback === 'function' && callback();
}
// CASE 3. 함수의 반환 값으로 함수를 내보낼 수 있다. (객체도 가능)
var fn = (function(global){
  'use strict';
  return function(){};
}(window));
// CASE 4. 객체의 속성으로 함수를 설정할 수 있다. (메소드)
var obj = {
  member: fn
}
// CASE 5. 배열의 원소(Item)로 함수를 메모리할 수 있다.
var fnStack = [obj.member];
```


## BOM(Browser Object Model)
- 웹 브라우저 창 세선 (window {})
- 사용자가 창(탭)을 생성하면 내부적으로는 new Window(); // window {}

- 전역 객체: window 객체
```js
console.log(window);
```
### 스크린 객체
- 속성(메서드)
- 사용자가 보는 화면의 정보를 가진 객체
- 가로(너비), 세로(높이) 정보
- 가용(Avail) 가능한 가로/세로 정보
- 컬러 심도 정보
```js
window.screen
```

### 로케이션 객체
```js
window.location

location.protocol // https: //
location.host // www.google.co.kr
location.search // ?gfe_rd=cr&ei=yBY6WfKrJ6WL8Qf-oKj4Dw
location.hash // #newwindow=1&q=%EC%B4%88%EB%B3%B5
location.href // https://www.google.co.kr/?gfe_rd=cr&ei=yBY6WfKrJ6WL8Qf-oKj4Dw#newwindow=1&q=%EC%B4%88%EB%B3%B5
```

### 히스토리 객체
```js
var his = window.history;
// 메서드
his.back();
his.forward();
his.go();
```

### 내비게이터 객체
#### 브라우저 스니핑
```js
window.navigator
// 온라인/오프라인 유무 (불리언 값 반환)
function isOnline() {
  return window.navigator.onLine;
}
function isWindows() {
  return window.navigator.platform.toLowercase().indexOf('win') > -1;
}
function isMac() {
  return window.navigator.platform.toLowercase().indexOf('mac') > -1;
}

// 브라우저 식별
// https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/User-Agent/Firefox
// https://msdn.microsoft.com/en-us/library/ms537503(v=vs.85).aspx
// https://dev.opera.com/blog/opera-user-agent-strings-opera-15-and-beyond/
function whatIsBrowser() {
  var ua = window.navigator.userAgent.toLowerCase();
  var browsers = ['chrome', 'safari', 'firefox', 'ie', 'opera'];
  var check_browsers = {
    chrome: false,
    safari: false,
    firefox: false,
    ie: false,
    opera: false
  };
  for ( var i=0, l=browsers.length; i<l; ++i ) {
    var browser = browsers[i];
    switch(browser) {
      case 'chrome':
        check_browsers.chrome = ua.indexOf(browser + '/') > -1;
      break;
      case 'safari':
        check_browsers.safari = ua.indexOf('chrome/') === -1 && ua.indexOf(browser + '/') > -1;
      break;
      case 'firefox':
        check_browsers.firefox = ua.indexOf(browser + '/') > -1;
      break;
      case 'ie':
        check_browsers.ie = ua.indexOf('rv:11.0') > -1 || ua.indexOf('trident/') > -1 || ua.indexOf('msie/') > -1;
      break;
      case 'opera':
        check_browsers.opera = ua.indexOf('opr/') > -1;
      break;
    }
  }
  return check_browsers;
}

function isChrome() {
  return window.navigator.userAgent.toLowerCase().indexOf('chrome') > -1;
}
```


### 도큐멘트 객체
```js
window.document
```

## DOM(Document Object Model)
### 역사??
#### DOM Lv0 (Legacy DOM)
- 초창기 JavaScript 환경에서 사용되던 저수준의 문서 객체 모델
```js
(function(global){
  'use strict';

  var document = global.document;

  // links
  document.links;
  // anchors
  document.anchors;
  // images
  document.images;
  // forms
  document.forms;

})(window);
```
#### 과도기 DOM
- 표준 없이 기술 경쟁하던 시대
- 문서의 모든 객체에 접근이 가능해졌고, CSS를 사용하여 속성을 변경 제어할 수 있게 되었다.

- document.all()   VS   document.layers()


#### DOM Lv1
- 기업 간 합의를 통해 표준화가 진행되던 시대
```js
doucment.getElementById() // => Node
(ElementNode || doucment).getElementsByTagName()//  => NodeList
```


#### DOM Lv2
- 화합이 무너지고 기업간 경쟁이 다시 점화되는 시기
- Events 모델 -> 업그레이드

- Microsoft 사의 기술 문서
- 이벤트 버블링만 지원
```js
window.event
window.event.srcElement
.attachEvent()
.detachEvent()
```

- W3C 표준 기술 문서
- 이벤트 캡쳐링/버블링 모두 지원
- 함수 내에 event 객체를 전달
```js
event.target
.addEventListener()
.removeEventListener()
```

## 실습
```html
<!DOCTYPE html>
<!-- 에밋 단축키 -->
<!-- -->
<!--[if IE 6]><html lang="ko-KR" class="no-js ie lt-ie10 lt-ie9 lt-ie8 ie6"><![endif]-->
<!--[if IE 7]><html lang="ko-KR" class="no-js ie lt-ie10 lt-ie9 lt-ie8 ie7"><![endif]-->
<!--[if IE 8]><html lang="ko-KR" class="no-js ie lt-ie10 lt-ie9 ie8"><![endif]-->
<!--[if IE 9]><html lang="ko-KR" class="no-js ie lt-ie10 ie9"><![endif]-->
<!--[if !IE]><!-->
<html lang="ko-KR" class="no-js no-ie modern">
<!--<![endif]-->
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>함수 Part 3, 배열, 객체 &lt; JavaScript 학습</title>
  <style>
    /* 해킹이 아닌, 필터링 */
    /*.lt-ie10 #products {  }
    .lt-ie8 #products {  }
    .ie7 #products {  }
    .ie6 #products {  }*/
  </style>
  <!-- 데이터 로드 -->
  <script src="study/data.js"></script>
  <!-- FDS 라이브러리 파일 로드 -->
  <script src="../LIBRARY/FDS.js"></script>
  <!-- 학습 파일 로드 -->
  <!--<script src="./study/01.functions.js"></script>-->
  <script src="./study/04.DOM.js"></script>
</head>
<body>
<!--ul#products>li.product-item*>a-->
  <ul id="products">
    <li class="product-item is-phone"><a href="">phone</a></li>
    <li class="product-item is-bag"><a href="">bag</a></li>
    <li class="product-item is-hat"><a href="">hat</a></li>
    <li class="product-item is-car"><a href="">car</a></li>
    <li class="product-item is-book"><a href="">book</a></li>
  </ul>

  <!--데모 파일-->
  <!--HTML Parser가 JavaScript 코드를 해석하거나, 서버에 요청할 경우는 일을 안한다.-->
  <script>
    (function(global, document){
      'use strict';

      // 문서객체에서 id 속성 값이 products 인 요소노드를 찾아 변수에 할당
      var products = document.getElementById('products');
      // 변수 products에 참조되어 있는 문서 객체 내부에서 li 요소노들을 수집하여
      // 변수 products_items에 참조
      var products_items = products.getElementsByTagName('li');
      // console.dir(products_items);
      var changeLinkColor = function() {
        this.style.color = 'lightblue';
      };

      // products 요소노드 내부에 모든 li를 수집한 후,
      // 수집된 집합의 아이템을 순환 처리한다.
      for ( var i=0, l=products_items.length; i<l; ++i ) {
        var item = products_items.item(i);
        var link = item.getElementsByTagName('a')[0]; // return ElementNode
        // link 초기 스타일 설정
        link.style.outline = 'none';
        // 아이템 내부의 하이퍼링크 요소를 찾아서 이벤트를 바인딩한다.
        link.onfocus = changeLinkColor;
      }

    })(window, window.document);
  </script>
</body>
</html>

```