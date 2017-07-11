FDS-40-jQuery,pug
========


## package.json 파일 설명
- github 해당 폴더를 당겨온 뒤 package.json 파일이 있는 위치에서 npm 설치를 하면
- package.json 파일 내에서 설정한 것들을 이용하여  node_modules폴더가 설치된다.
```bash
$ npm install
```
- 실행 (여러개의 명령어 실행 시키는 dev)
```bash
$ npm run dev
```
- sass에 작성하면 자동으로 css가 만들어지고, es6를 만들면 자동으로 es5로 나오고, pug쓰면 html 컴파일 해준다. 크로스 브라우징 문제가 없다.

## ES6 복습
- es6를 es5로 컴파일해주는데, 지역변수를 써봤자 es5에는 전역변수가 되기때문에 아직까지는 iife 문법을 써준다.
### 화살표 함수
```js

```

## 템플릿 엔진
- 템플릿을 읽어 엔진의 문법과 설정에 따라서 파일을 HTML 형식으로 변환시키는 모듈
- 동적으로 마크업 가능

### pug
- 참고: <https://pugjs.org/api/getting-started.html>
- node.js의 express 프레임 워크
- sass 문법과 유사
```pug
<!DOCTYPE html>
html(lang="en")
  head
    meta(charset="UTF-8")
    title jQuery 학습

  body

  .app.container
    .columns
      .column.is-6.is-offset-3.main
        h1.title.is-1 Hi jQuery :-)
        p.subtitle.is-4 write less do more.

  script(src="./js/main.js")
```
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8"/>
  <title>jQuery 학습</title>
</head>
<body>
  <div class="app container">
    <div class="columns">
      <div class="column is-6 is-offset-3 main">
        <h1 class="title is-1">Hi jQuery :-)</h1>
        <p class="subtitle is-4">write less do more.</p>
      </div>
    </div>
  </div>
  <script src="./js/main.js"></script>
</body>
```

### ejs
- 참고: <http://ejs.co/>
- 참고: <https://velopert.com/379>
- node.js의 express 프레임 워크
```html
<!--<% 자바스크립트 코드 %>-->
<!--<% 출력 할 자바스크립트 객체 %>-->
<html>
  <head>
  <!-- 라우터에서 title을 받아와서 출력 -->
  <title><%= title %></title>
  <link rel="stylesheet" type="text/css" href="css/style.css">
  </head>
  <body>
    <h1>Loop it!</h1>
    <ul>
    <!-- 루프문 -->
      <% for(var i=0; i<length; i++){ %>
        <li>
          <%= "LOOP" + i %> 
        </li>
      <% } %>
    </ul>
  </body>
</html>
```

## sass 프레임워크
- sierra: <http://sierra-library.github.io/>
- iotacss: <https://www.iotacss.com/>

## jQuery
- 참고: <http://api.jquery.com/>
- 버전1은 IE 하위 버전 지원하고, 버전2부터 IE 9+ 지원한다.
- api 에서 returns: jQuery가 나오면 메서드 체이닝이 가능

## yarn
- 참고: <https://yarnpkg.com/lang/en/>
- npm보다 빠르고 같이 쓸 수 있다.

## CDN(Content Delivery Network)
- 참고: <http://88240.tistory.com/351>
- 콘텐츠를 효율적으로 전달하기 위해 여러 노드를 가진 네트워크에 데이터를 제공하는 시스템을 말한다.
- 인터넷 서비스 제공자에 직접 연결되어 데이터를 전송하므로, 콘텐츠 병목현상을 피할 수 있다.
- 여러곳의 IDC 또는 ISP에 동일한 컨텐츠를 올려놓고, 접속자가 사용하는 인터넷전용회선의 종류에 따라 가장 가까운 곳에서 컨텐츠를 불러들일 수 있도록 지원하는 서비스
- 영화와 게임처럼 용량이 큰 콘텐츠를 효율적으로 이용자에게 배달하는 통신망 체계. 제한적인 통신망 자원으로 더 많은 콘텐츠를 안정적으로 전송하는 게 관건. 이를 위해 컴퓨팅 서버를 여러 개 마련해 통신량이 한곳에 몰리지 않게 한다.

### jQuery를 사용하는 방식 로컬 vs CDN
- 직접 받아서 로컬로 쓰는 방식
  ```html
  <script src="/node_modules/jquery/dist/jquery.min.js"></script>
  ```
- CDN 방식
  - 한번 받으면 캐시에 저장을해서 다음에는 받지 않는다.
  - `http:`를 생략하는 이유: 브라우저는 http 와 https 를 통해서 가져온 같은 리소스를 다르게 취급함. 그래서 리소스를 캐싱할 때 다르게 저장함. 이전에 http:// 로 접속해서 파일을 읽어와서 나중을 위해 디스크에 캐싱해 두었더라도, https:// 로 같은 파일에 접근할 경우, 같은 파일임에도 불구하고 캐싱해 둔 파일을 이용하지 못한다. 앞에 http: 나 https: 를 생략하고 지정을 해주면, 현재 문서가 지정된 프로토콜이 http 인지, https 인지에 따라, 적합한 리소스를 이용하게 된다. 
  ```html
  <script src="//unpkg.com/jquery"></script>
  ```


## Ajax GET
```js
// JSON:
// https://api.myjson.com/bins/f0etn
((global, $) => {
  'use strict';

  let api_id = 'f0etn';
  let api_address = `https://api.myjson.com/bins/${api_id}`;

  // Ajax GET
  $.get(api_address).then(data => {
    console.log(data);
  });

})(window, window.jQuery);
```

## jQuery 버전 출력
- v 3.2.1
```js
;(function(global, $){
  'use strict';

  console.log('jQuery 버전? $().jquery = ', $().jquery);
  console.log('jQuery 버전? $.fn.jquery = ', $.fn.jquery);
  console.log('jQuery 버전? $.prototype.jquery = ', $.prototype.jquery);
  console.log('jQuery 버전? jQuery.prototype.jquery = ', jQuery.prototype.jquery);

})(window, window.jQuery);
```

## CSS 조작
```js
;(function(global, $){
  'use strict';

  // 메서드 체이닝이 가능한 이유는
  // jQuery 객체가 메서드마다 반환되기 때문
  // > 모든 메서드가 가능한 것은 아님 (API 문서 확인)

  // 팩토리 함수
  // CSS 선택자를 전달
  $('h1')
    // CSS 속성을 제어하는 jQuery 객체(인스턴스)의 메서드를 사용
    .css('color', 'tan')
    .addClass('is-3')
    .removeClass('is-1');

})(window, window.jQuery);
```

## 인스턴스 메서드 검증
```js
;(function(global, $){
  'use strict';

  console.log('jQuery.prototype.css', !!jQuery.prototype.css); // true
  console.log('jQuery.prototype.addClass', !!jQuery.prototype.addClass); // true
  console.log('jQuery.prototype.removeClass', !!jQuery.prototype.removeClass); // true
  console.log('jQuery.prototype.radioClass', !!jQuery.prototype.radioClass); // false -> 만들면 되지!

})(window, window.jQuery);
```

## DOM Node 전달
```js
;(function(global, $){
  'use strict';

  // DOM Node 전달
  // DocumentNode
  // Host Object 전달
  // Document {}
  // .on() jQuery 인스턴스 메서드
  // $(document).on('click', function(e) {
  $(document).on('click', e => {
    console.log(e.target);        // Event Object 의 target 속성 값은?
    console.log(e.currentTarget); // Event Object 의 currentTarget 속성 값은?
    // 중요!!!!!
    // 함수 값(리터럴)에서는 this가 이벤트의 주인을 가리키지만,
    // 화살표 함수 내 this는 상위 컨텍스트를 가리킨다.
    console.log(this);            // Arrow Function 내부의 this는?
  });
  // Window {}
  // 사용자가 스크롤 이벤트를 발생시키면,
  // 콜백 함수가 실행된다.
  let $window = $(window);
  let $main   = $('.main');

  $window.on('scroll', function(){
    $window.scrollTop() > 123 ?
    // this.scrollTop() > 123 ?
      $main.addClass('is-fixed') :
      $main.removeClass('is-fixed');
  });
  // }.bind($window));

})(window, window.jQuery);
```

## 팩토리 함수
```js
;(function(global, $){
  'use strict';

  // 요소노드
  let body = global.document.body;
  let $body = $(body);
  let style_map = {
    fontSize: '32px',
    'margin-bottom': '+=40px',
    'background': 'url("//placehold.it/1920x900/000/fff") 0 0 / cover no-repeat'
  };

  $body.css(style_map);

  // 노드리스트
  let $body_children = $(body.children);
  $body_children.attr('data-children-of-body', 'yes');

  // 배열
  // $().each()는 네이티브 forEach() 와 달리 index, item 순.
  // .attr() 메서드   VS   .data() 메서드
  $([document.documentElement, document.body]).each((index, el)=>{
    let $el = $(el);
    if ( el.localName === 'html' ) {
      $el.data('is-root', 'yes');
    } else {
      $el.data('is-root', 'no');
    }
    console.log($el.data('is-root'));
  });

  // jQuery 객체
  // jQuery 팩토리 함수에 jQuery 객체를 전달할 수도 있다.
  // $( $body )

  // HTML 문자열
  let $dim = $('<div/>', {
    'class': 'dim',
    'on': {
      'click': e => $(e.target).remove(),
      'mouseenter': e => $(e.target).css('background-color', 'hsla(249.7, 100%, 65.9%, 0.7)'),
      'mouseleave': e => $(e.target).css('background-color', $dim.data('original-dim-bg'))
    }
  })
  .prependTo($body);

  $dim.data('original-dim-bg', $dim.css('background-color'));

})(window, window.jQuery);
```



## iife 다른 방법
### 화살표 함수
```js
((global, $) => {
  'use strict';
  // code
})(window, window.jQuery);
```
### jQuery 
```js
jQuery(function($){
  // code
});
```
### ready() 메서드 이용
- ready 문처럼 동작
- 참고: <http://api.jquery.com/ready/>
- 문서가 준비되면 (document ready) 콜백함수 코드 실행
```js
jQuery(document).ready(function($){
  // code
});
```
### noConflict 메서드 이용
```js
jQuery.noConflict()(function($){
  // code
});
```


## jQuery Core
### jQuery.noConflict()
- 포기하는거
```js
jQuery === $ //true
jQuery.noConflict(true); // removeAll -> window에 있는 window.jQuery까지 포기하겠다.
let $$ = jQuery.noConflict(true); // unfined
window.jQuery // unfined
// 그러나 $$는 jQuery를 기억하고 있음
$$ // jQuery
```

### jQuery.holdReady()
- 인자로 true -> 함수가 끝난 후 false
- returns: undefined
- 비동기 통신할 때 쓴다.
```js
((global, $) => {
  'use strict';

  let api_id = 'f0etn';
  let api_address = `https://api.myjson.com/bins/${api_id}`;

  // jQuery Ready()를 붙잡자(hold)
  console.log('jQuery Ready()를 붙잡자(hold: true)');
  $.holdReady(true);

  // Ajax GET
  $.get(api_address).then(data => {
    console.groupCollapsed('jQuery Ajax 데이터 로드');

    console.log(data);

    console.groupEnd('jQuery Ajax 데이터 로드');
    console.log('jQuery Ready()를 놓아주다(hold: false)');
    $.holdReady(false); // Excute Ready Function
  });

})(window, window.jQuery);
```

## CSS
### .addClass()
        //- $('body').children().attr('class', 'body-children'); // 기존의 클래스를 새로운 클래스로 대체
        $('body').children().addClass('body-children');
- 인자로 className,function
- return: jQuery
- .addClass(function)
- .find()
- $("p").last()
- $("p:last") -> 수집된 p중에 마지막 애
  ```js
  ;(function(global, $){
    'use strict';
    
    // addClass() + function
    // (index, currentClassName) => String
    $('.app').addClass((index, name) => {
      // console.log(index, name); // 0 "app container"
      let names = name.split(' ');
      console.log(names);
      let convert_names = names.map(name => {
        return `-${name}-*`;
      });
      console.log(convert_names); // '[-app-]', '-container-'
      convert_names = convert_names.join(' ');
      console.log(convert_names); // '*-app-* *-container-*'
      return convert_names;
    })
    .find('*').addClass(index => 'child-' + index);


  })(window, window.jQuery);
  ```

## hasClass()
- boolean 반환. -> 메서드 체이닝에 쓰지 않고 조건문에 쓴다.
## .append()

## 실습 (Accordion UI)
- 참고: <https://jqueryui.com/accordion/>
- 모바일 환경에서 주로 사용
```html
<!DOCTYPE html>
html(lang="en")
  head
    meta(charset="UTF-8")
    meta(name="viewport", content="width=device-width, initial-scale=1")
    meta(http-equiv="X-UA-Compatible", content="ie=Edge")
    title jQuery 학습
    link(rel="stylesheet", href="/node_modules/bulma/css/bulma.css")
    link(rel="stylesheet", href="./css/main.css")
    script(src="/node_modules/jquery/dist/jquery.min.js")
    script.

  body

    .app.container.wrapper.yamoo9-code
      .columns
        .column.is-6.main
          h1.title.is-1 Hi jQuery :-)
          p.subtitle.is-4 write less do more.

          //- 데이터 정의
          -
            var accordion_data = {
              'general': {
                'links': ['dashboard', 'customers']
              },
              'administration': {
                'links': ['team settings', 'manage your team']
              }
            }
          //- 믹스인 정의
          mixin accordion(data)
            article.ui-accordion.menu.box
              each links, label in data
                h4.menu-label
                  a.box(href)= label
                ul.menu-list
                  each link in links
                    li
                      each content in link
                        a(href)= content

          //- 믹스인 사용 (복제한 만큼 나타난다.)
          +accordion(accordion_data)

    script(src="./js/main.js")
```
```js
;(function(global, $){
  'use strict';

  let $component, $lists, $labels;

  // 컴포넌트 아코디언 초기화 함수
  function init(){
    $component = $('.ui-accordion');
    $lists = $component.find('.menu-list');
    $labels = $('.menu-label a', $component);
    // 리스트를 모두(필터링 할 경우, 필터링 대상만) 감춤
    // $lists.filter((index, el)=>{
    //   return index > 0;
    // }).hide();
    $lists.hide();
    // 이벤트 바인딩
    bind();
    $labels.eq(0).trigger('click');
  }
  function bind() {
    $('.menu-label a', $component).on('click', toggleList);
  }
  function toggleList(e) {
    e.preventDefault();
    // this.parentNode.classList.add('is-active');
    let time = 300; // 300/1000 = 0.3s
    let $this = $(e.target);
    let $list = $this.parent().next();
    if ( $list.css('display') === 'none' ) {
      $list.show(time);
      $this.addClass('is-active');
    } else {
      $list.hide(time);
      $this.removeClass('is-active');
    }
  }
  // 초기화 실행
  init();

})(window, window.jQuery);
```

