FDS-27-HTML에서DOM,DOM 선택,탐색 유틸리티 함수 정의
========

## 테스트

### BOM 객체
- navigate -> 가 아니라 navigator!!
- window
- history
- screen
- document
- location

### DOM Lv0 함수
- document.all (쓰지 마라)

### JavaScript 일급 객체인 이유
- 변수에 할당 가능하다.
- 함수의 인자로 함수를 전달할 수 있다. -> 콜백
- 함수의 반환 값으로 함수를 내보낼 수 있다. -> 클로저
- 객체의 속성에 함수를 설정할 수 있다. -> 메서드
- 배열 아이템으로 메모리가 가능하다. -> 배열에 함수를 쌓아놓고서 함수를 언제든 실행할 수 있다.

### 'use strict' 선언
- 함수 내 this -> 그냥 암시적 방법으로 선언하면 undefined / new를 붙여서 명시적으로 할 경우 괜찮음.
- 선언되지 않은 변수에 접근 또는 값을 할당하고자 할 경우 오류 발생
- new를 사용하지 않고 생성자 함수를 사용할 경우 오류를 발생하게 한다.
- 엄격 모드를 지원하지 않는 구형 웹 브라우저는 이를 문자열로 인식할 뿐 오류는 발생하지 않는다.

### recall()함수 실행 결과 값
- 재귀함수 : 자신을 다시 호출
```js
var recall = function () {
    var _data = [];
    return function(str){ // 'use case design project'
        var str_data = str.split(' '); // ['use', 'case', 'design', 'project'] => 빈 문자열을 경계로 나뉘게 됨
        var first_str = str_data.shift(); // ['case', 'design', 'project'] => 첫 번째 요소를 반환시키고 원본도 바뀐다. (str_data = 'use') first_str = ['use']
        // first_str이 참인 조건 : ??? => 빈 배열이 아니면
        first_str && _data.push('*' + first_str + '*'); // first_str ('use')이 참이면 && _data 배열에 넣어라. => _data = ['*case*']
        first_str && recall(str_data.join(' ')); 
        // str_data를 다시 한 문장으로 만들어서 recall함수의 인자로
        // if를 명시적으로 말해주지 않지만 조건문
        // first_str이 거짓이 되는 순간 뒤에 recall이 실행되지 않으면서 끝난다.
        return _data.join(' ');
        // 이미 _data에 축적되어 있는것들이 반환된다.
    };
}();

recall('use case design project');
// ['*use* *case* *design* *project*']
```

### 함수 내에서만 접근 가능한 전달인자 집합 객체
- `arguments`
- 함수에 전달된 인수에 해당하는 Array같은 객체
- 모든 함수 내에서 이용 가능한 지역 변수
- length 빼고는 어떠한 Array의 속성이 없다.


### <script>요소를 <head> 내에서 불러올 때 주의해야 할 점
- 문서 객체에 접근하고자 할 경우, null이 도출될 수 있다.




## HTML & DOM
- html문서에 DOM파일을 로드할 때 `<head>`태그 안에 모든 js파일을 넣으면 body에서 실행되는 구문은 아직 실행되지 않았기 때문에 null이 발생한다.
- 예시(head태그 안에 js파일을 넣었을 경우)
```html
<head>
    <!--이하 생략-->
    <script src="study/data.js"></script>
    <script src="../LIBRARY/FDS.js"></script>
    <script async src="./study/DOM.Script.js"></script>
    <!-- head태그 안에 선언-->
</head>
<body>
    <div id="target-parent">
        <h1>
            <abbr title="Document Object Model">DOM</abbr> Script
            <!-- abbr요소 : abbreviation, 약어 혹은 두문자어 -->
            <!-- 속성값 title : 약어의 축약되지 않은 텍스트를 값으로 가지며, 원형 이외의 다른 텍스트는 포함할 수 없다. -->
        </h1>
    </div>
</body>
```
```js
(function(global, document){
    'use strict';

    var html, head, body;

    html = document.documentElement; 
    head = document.head;
    body = document.body;

    console.log('html: ', !!html); // true 접근가능
    console.log('head: ', !!head); // true 접근가능
    console.log('before load - body: ', !!body); // null (접근불가): 스크립트가 실행되는 동안에 body가 만들어지지 않아서 -> 이벤트를 사용해서 해결할 수 있다.
}(window, window.document));
```

### window.onload 이벤트
- 이벤트 : load
- 이벤트 핸들러 : onload
- 페이지가 로드될 때 특정 함수를 호출시 사용
```js
(function(global, document){
    'use strict';
    var html, head, body;
    html = document.documentElement; 
    head = document.head;
    body = document.body;

    // 초기화 함수
    function init() {
        html = document.documentElement; 
        head = document.head;
        body = document.body;

        console.log('html: ', !!html); // 접근가능
        console.log('head: ', !!head); // 접근가능
        console.log('after load - body: ', !!body); // 접근가능
    }

    // window 객체의 onload 이벤트 속성에 함수를 할당 (init함수 종료 시점에 함수 실행)
    // 여기서 init(); 이라고 하면 안됨 -> 실행되서 onload에 undefined가 담기게 된다.
    window.onload = init;

}(window, window.document));
```
### body태그 끝 부분에서 js파일 불러오기
- 가장 좋은 방법
```html
<body>
<!--이하 생략-->
  <script src="./study/DOM.Script.js"></script>
</body>
```
### 하지만 꼭 head태그 안에 js파일을 불러와야 할 경우
- 참고 : <http://www.growingwiththeweb.com/images/2014/02/26/async-vs-defer-twitter.png>
- `defer`: 페이지 파싱이 완료된 후에 스크립트를 실행. 불리언 속성
- `async`:  가능한한 빨리 스크립트를 비동기적으로 실행. 불리언 속성
- async 속성을 사용하면서 defer 속성을 함게 사용할 수 있다. defer 속성을 지원하는 일부 구형 브라우저가 존재하기 때문. 이 경우 async 속성은 무시되고, defer 속성을 따르게 되어 스크립트를 비동기적으로 실행. / 그리고 둘 다 하위 브라우저 크로스 브라우징 이슈가 있어서 되도록 안 쓰는게 좋다.
```js
<script type="text/javascript" src="navigation.js" async defer></script>
```


## instance, class
- 인스턴스는 객체를 생성하기 위해 만들어진 또 다른 객체. 이런 인스턴스를 만들기 위해서는 객체지향에서 말하는 클래스(Class)가 필요하다.
- 클래스는 다른 객체를 만드는 틀.
- 자바스크립트는 객체지향 언어이고, 같은 클래스(생성자 함수)의 객체가 여러 개 있을 수 있으며, 각 객체는 해당 클래스의 인스턴스에 해당한다.
- 원래의 객체가 가지고 있는 프로퍼티(property)와 메소드(method)를 상속받는다.


## Core(XML) DOM
- Ajax 요청 <- 데이터() 
- 우리는 HTML DOM을 사용할 것이지만, Core DOM을 사용하는 회사를 만날수도 있다.

## `item(index)`메서드 
- 컬렉션의 현재 항목을 반환. Enumerator 개체(컬렉션에서 항목을 열거할 수 있도록 설정)
- IE에서만 지원???(참고: <https://msdn.microsoft.com/ko-kr/library/e9ka710x(v=vs.94).aspx>)
- 비어 있거나 현재 항목이 정의되지 않은 경우 undefined를 반환합니다.
- 배열 메서드 5가지 참고 : <http://blog.kazikai.net/?p=16>

## `getElementById(name)`
- html 문서에서 지정된 아이디 속성을 포함하는 단 하나의 요소를 참조
## `getElementsByTagName(name)`
- 전체 문서에서 매개변수 값의 요소 엘리먼트를 찾을 수 있다.
- id와 다르게 여러개의 같은 이름을 사용하는 태그를 얻게 된다.
```js
var document = global.document;
var html = document.getElementsByTagName('html').item(0);
var head = document.getElementsByTagName('head').item(0);
var body = document.getElementsByTagName('body').item(0);
// DOM API를 사용해서 노드리스트에 접근한 후, 개별 아이템을 추출
var headline = document.getElementsByTagName('h1')[0];
var abbr_in_headline = headline.getElementsByTagName('abbr')[0]; 
// 다른 요소 엘리먼트들과 달리 headline 요소 안에 있다는 것을 주목
```

## Node Info
```js
var target_parent, target_headline, target_abbr;

target_parent   = document.getElementById('target-parent'); // <div>
target_headline = target_parent.firstChild; // <h1>
target_headline = target_parent.getElementsByTagName('h1').item(0);
target_abbr     = target_headline.firstChild; // <abbr>
target_abbr     = target_headline.getElementsByTagName('abbr')[0];

console.log(,target_parent.nodeName);   //  nodeName : DIV, tagName (DOM Lv3까지 표준) -> 대문자라는것 잊지말자.
console.log(target_parent.localName);   //  lacalName: div  // IE 검증 필요 -> 소문자로 나온다 그러나 IE,safari 에서는 검증이 안된다.
console.log(target_parent.nodeType);    //  nodeType : 1 === document.ELEMENT_NODE
console.log(target_parent.nodeValue);   //  nodeValue: null -> nodeValue를 갖지 않는다.
 
console.log(,target_headline.nodeName); //  nodeName : #text | H1
console.log(target_headline.nodeType);  //  nodeType : 3     | 1
console.log(target_headline.nodeValue); //  nodeValue: | null -> 텍스트노드는 nodeValue를 가진다.
```
- 요소노드는 nodeType 속성 값이 1 이며, nodeName 값은 요소의 이름을 대문자로 반환한다.
- 요소노드는 nodeValue 속성 값을 가지지 않지만, textContent, innerText 속성으로 값을 도출할 수 있다.
- 텍스트노드는 nodeType 속성 값이 3 이며, nodeName 속성 값은 '#text' 를 반환한다.
- 텍스트노드는 nodeValue 속성 값을 문자 값으로 반환한다.

### nodeName 프로퍼티
- 엘리먼트 노드의 nodeName은 태그의 이름과 같다.
- 속성 노드의 nodeName은 속성의 이름이다.
- 텍스트 노드의 nodeName은 항상 #text이다.
- 문서 노드의 nodeName은 항상 #document이다.

### nodeValue 프로퍼티
- 엘리먼트 노드의 nodeValue는 undefined다.
- 텍스트 노드의 nodeValue는 텍스트 자체다.
- 속성 노드의 nodeValue는 속성 값이다.

### 노드의 정보
- `NODE.nodeType`       : 노드의 타입(대문자). 읽기전용 (요소노드 = 1, 속성노드 = 2, 텍스트노드 = 3, 주석노드 = 8)
- `NODE.localType`      : 노드의 타입을 소문자로. 읽기전용. 크로스 브라우징 이슈
- `NODE.nodeName`       : 노드의 이름
- `NODE.nodeValue`      : 노드의 값
- `NODE.parentNode`     : 자식노드의 부모노드
- `NODE.firstChild`     : 부모노드의 첫번째 자식노드
- `NODE.lastChild`      : 부모노드의 마지막 자식노드
- `NODE.previousSibling`: 이전 형제노드
- `NODE.nextSibling`    : 다음 형제노드
- `NODE.childNodes`     : 부모노드의 모든 자식노드들 (노드의 배열이 반환됨)
- `NODE.children`       : 부모노드의 모든 자식노드들 (요소노드만)
- `attributes`          : 노드의 속성, 속성 노드의 리스트가 반환됨


## DOM 검증 API
- 노드.nodeType (요소노드 = 1, 속성노드 = 2, 텍스트노드 = 3, 주석노드 = 8)
- 요소노드(Element)인지 아닌지
```js
function isElNode(node) {
    return node.nodeType === 1;
}
function validateElNode(el_node) {
    if ( !el_node || !isElNode(el_node) ) { 
    throw '요소노드를 반드시 전달해야 합니다';
    }
}
```

## DOM 선택 API
- `context` : 무엇을 가리키는것?
```js
function id(name) {
    validateError(name, '!string', '전달인자는 문자여야 합니다.');
    return document.getElementById(name);
}
// 특정 태그 전부
function tagAll(name, context) {
    validateError(name, '!string', '전달인자는 문자여야 합니다.');
    if ( context && !isElNode(context) ) {
    throw '두번째 전달인자는 요소노드여야 합니다.';
    }
    return (context||document).getElementsByTagName(name);
}
// 특정 태그의 몇 번째(index) 태그만
function tag(name, context) {
    return tagAll(name, context)[0];
}
```
```js
;(function(global, $){
    'use strict';

    var document = global.document;
    var target_parent   = $.id('target-parent'),
        target_headline = $.tag('h1'),
        target_abbr     = $.tag('abbr',target_headline),
        all_els         = $.tagAll('*', target_parent);
})(window, window.FDS); // DI 주입
```

## 부모노드 탐색 API
- `parentNode`
```js
// 아래 시작부분에 ;(세미콜론)은 IIFE패턴 병합 시 발생할 수 있는 오류를 예방하기 위해 넣어준다.
;(function(global, document){
    'use strict';
    
    // 부모노드(parentNode) 탐색
    console.log('headline 요소의 부모의 부모의 부모는?',headline.parentNode.parentNode.parentNode); // document
    console.log('headline 요소의 부모의 부모의 부모는 document 객체?',headline.parentNode.parentNode.parentNode === document); // true
    console.log('headline 요소의 부모의 부모의 부모인 document 객체의 부모는?',headline.parentNode.parentNode.parentNode.parentNode); // null
    console.log('document 객체의 부모는?',document.parentNode); // null -> 노드와 부모는 다른 개념이다. document의 부모는 window지만, document 객체의 최상위는 document이기 때문에 null이 나온다.
    console.log('headline 요소의 부모노드는?',headline.parentNode); // body
    console.log('abbr 요소의 부모노드는?',abbr_in_headline.parentNode); // h1

}(window));
```

## 자식노드 탐색 API
- html문서에서 줄바꿈을 할 경우 공백문자가 생긴다. DOM에서는 공백문자도 노드이기때문에 자식요소로 공백문자(텍스트노드)를 불러올 수 있다.
- 이 때문에 자식노드를 탐색하기 어렵다 -> 요소노드이냐? 텍스트요소이냐? 물어보는 재귀함수를 만들어 요소노드인 첫번째 자식노드만 불러올 수 있다.
```html
<body>
  <!--아래와 같은 마크업은 공백이 없어 첫번째 자식노드가 <abbr> 이지만... -->
  <h1><abbr title="Document Object Model">DOM</abbr> Script</h1>

  <!--아래와 같은 마크업은 공백이 있어 첫번째 자식노드가 #text (텍스트 노드)이다. -->
  <!--childNodes, children 속성은 자식 노드만 가져온다.-->
  <div id="target-parent">
    <h1>
      <abbr title="Document Object Model">DOM</abbr> Script
    </h1>
  </div>
</body>
```
```js
console.log('headline의 첫번째 자식은?', headline.firstChild); // 공백이 없다면 ? <abbr> : #text
console.log('headline의 마지막 자식은?', headline.lastChild);  // ' Script' (텍스트 노드)
```
### 자식노드들 중에서 요소노드만 골라내기
```js
function onlyElementNodeCollection(el) {
    if ( !el || el.nodeType !== 1 ) { throw '요소노드를 전달하세요'; }
    var el_childs = el.childNodes;
    var collection = [];
    // 순환문을 돌려서 요소 노드만 별도로 수집한 객체를 변수에 참조해보자.
    // 노드.nodeType (요소노드 = 1, 속성노드 = 2, 텍스트노드 = 3, 주석노드 = 8)
    for ( var i=0, l=el_childs.length; i<l; i++ ) {
    var child = el_childs[i];
    // if ( child.nodeType === 1 ) {
    //   collection.push(child);
    // }
    if ( child.nodeType !== 1 ) { continue; } // Jumping
    collection.push(child);
    }
    return collection;
}

var result = onlyElementNodeCollection(headline);

console.log(result);
```
### NODE.childNodes   VS   NODE.children
- `.childNodes` 는 모든 자식 노드를 반환
- `.children` 은 자식 중, 요소노드만 반환
```js
var target = document.getElementById('target-parent');
// console.log(target);
console.log(target.childNodes); // [text, h1, text] -> 텍스트노드, 요소노드 모두를 반환
console.log(target.children); // [h1] -> 요소노드만 반환

console.log(target.firstChild === target.childNodes[0]); // true
// 배열의 첫번째 인덱스[0]가 첫번째 자식요소
console.log(target.lastChild === target.childNodes[target.childNodes.length - 1]); // true
// target.childNodes.length - 1 => target.childNodes.--length(선감소로 표현할 경우)
// 배열의 길이에서 -1을 해주는 값이 배열의 마지막 요소의 인덱스 번호이기 때문에
```
### 첫번째 자식노드(firsChild)
- `firstElementChild`
- IE 9+ 만 지원
```js
function firstChild(el_node) { // 요소노드를 전달인자로 받는다.
   // 전달인자 검증
   if ( !el_node || el_node.nodeType !== 1 ) { // 전달인자가 거짓이거나 || 노드타입이 요소노드가 아닐 경우
     throw '요소노드를 반드시 전달해야 합니다';
   }
   return el_node.firstElementChild;
   // IE 8- 지원하는 크로스 브라우징 유틸리티 함수를 만든다면?
   // if ( 'firstElementChild' in Element.prototype ) { -> 왜 이렇게??
   if ( el_node.firstElementChild ) {
     return el_node.firstElementChild;
   } else {
     return el_node.children[0];
   }
}
```
- 최종(왜 이렇게 바꿨지???)
```js
var firstChild = function(){
    var _firstChild = null;
    // 조건을 1번만 확인
    if ( 'firstElementChild' in Element.prototype ) {
        _firstChild = function(el_node) {
            validateElNode(el_node);
            return el_node.firstElementChild;
        };
    } else {
        _firstChild = function(el_node) {
            validateElNode(el_node);
            return el_node.children[0];
        };
    }
    return _firstChild;
}();
```
### 마지막 자식노드(lastChild)
```js
var lastChild = function(){
    var _lastChild = null;
    // 조건을 1번만 확인
    if ( 'lastElementChild' in Element.prototype ) {
    _lastChild = function(el_node) {
        validateElNode(el_node);
        return el_node.lastElementChild;
    };
    } else {
    _lastChild = function(el_node) {
        validateElNode(el_node);
        var children = el_node.children;
        return children[--children.length]; // el_node.children[--children.length]
    };
    }
    return _lastChild;
}();
```
- 자식노드 실행
```js
;(function(global, $){
    'use strict';
    var document = global.document;

    // FDS 네임스페이스 객체의 first() 탐색 메서드 활용
    var target_first = $.first(target_parent);
    console.log('target_first:', target_first);
    var target_first_first = $.first(target_first);
    console.log('target_first_first:', target_first_first);

    var html_lastChild = $.last(document.documentElement);
    console.log('html_lastChild:', html_lastChild);
    var head_lastChild = $.last(document.head);
    console.log('head_lastChild:', head_lastChild);
    var body_lastChild = $.last(document.body);
    console.log('body_lastChild:', body_lastChild);
    
})(window, window.FDS); // DI 주입
```
## 형제노드 탐색 API
```js
function nextEl(el) {
    // 반복 구문 수행
    // el 다음 노드를 찾아서
    // 요소 노드인지 확인
    // 아니면... 다시
    // el 다음 노드를 찾아서
    // 요소 노드인지 확인

    // 무조건 한번은 실행시켜야 하니까 do..while문 사용
    do {
    el = el.nextSibling; // 무조건 실행해야되는 구문
    } while( el && el.nodeType !== 1 );
    return el;
}

function prevEl(el) {
    do {
    el = el.previousSibling;
    } while(el && el.nodeType !== 1);
    return el;
}
```
### 이전 형제노드 (previous)
```js
var previousSibling = function() {
    var _previousSibling;
    if ( 'previousElementSibling' in Element.prototype ) {
        _previousSibling = function(el_node) {
            validateElNode(el_node);
            return el_node.previousElementSibling;
        };
    } else {
        _previousSibling = function(el_node) {
            validateElNode(el_node);
            do {
                el_node = el_node.previousSibling;
            } while(el_node && !isElNode(el_node));
            return el_node;
        };
    }
    return _previousSibling;
}();
```
### 다음 형제노드 (next)
```js
var nextSibling = function($$) {
var _nextSibling;
if ( 'nextElementSibling' in $$ ) {
        _nextSibling = function(el_node) {
            validateElNode(el_node);
            return el_node.nextElementSibling;
        };
} else {
    _nextSibling = function(el_node) {
        validateElNode(el_node);
        do {
            el_node = el_node.nextSibling;
        } while(el_node && !isElNode(el_node));
    };
    return el_node;
    }
    return _nextSibling;
}(Element.prototype);
```

- 형제노드 실행
```js
;(function(global, document, $){ // 왜 여기에만 인자로 document를 더해줬을까?
    'use strict';

    // $.prev(), $.next()

    var head_first_next = $.next( $.first(document.head) );
    console.log('head_first_next:', head_first_next);

    var body_last_prev = $.prev( $.last(document.body) );
    console.log('body_last_prev:', body_last_prev);

})(window, window.document, window.FDS);
```



