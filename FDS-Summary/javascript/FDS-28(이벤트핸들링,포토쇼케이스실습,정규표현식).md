FDS-28-이벤트핸들링,포토쇼케이스실습,정규표현식
========

## 부모노드 찾기(숫자를 가지고 몇 칸 올라갈 수 있나?)
## location.hash
- `/` 에서 `#`(hash)로 바꿔줌
- `#`(hash) 는 콘솔창에서 `location.hash`로 접근 가능하고, 재설정도 가능하다.
```html
<div class="container">
  <ul id="study-content">
    <li><a href="/js-core" class="link-content">JavaScript Core</a></li>
    <li><a href="/dom-Script" class="link-content">DOM Script</a></li>
    <li><a href="/custom-js-lib" class="link-content">Custom JS LIBRARY</a></li>
    <li><a href="/js-framework" class="link-content">JS Framework</a></li>
  </ul>
</div>

<div class="container">
  <ul id="study-content">
    <li><a href="#js-core" class="link-content">JavaScript Core</a></li>
    <li><a href="#dom-Script" class="link-content">DOM Script</a></li>
    <li><a href="#custom-js-lib" class="link-content">Custom JS LIBRARY</a></li>
    <li><a href="#js-framework" class="link-content">JS Framework</a></li>
  </ul>
</div>
```

## node 정보
- id
- className
- title
- nodeName (tagName)
- nodeType (1,3)
- nodeValue (data)
- hasChildNodes() => 메서드 true & false 값 반환 has 는 있다없다 조건문에서 많이 사용됨

- document.getElementByClassName('link-content')



getElementById
getElementByTagName
getElementByClassName

// 얘네는 IE 8을 지원해
querySelector() -> 하나만
querySelectorAll() -> 모두

- querySelector()
selector들이 지정한 그룹과 일치하는 document 내의 첫 번째 element를 반환
 (depth-first를 우선적으로 사용해 문서의 노드들을 탐색합니다. 자식 노드의 양에 따라 첫 element를 검색하는 것을 순차적으로 반복하여 탐색합니다. )
querySelector(selector) // selecter를 사용하는 엘리먼트들 중에 첫번째를 반환 ".selector" 처럼 문자열로 된 css선택자를 넣아야한다.

- querySelectorAll()

```js
querySelector('ul li:last-child') // css 선택자와 비슷
querySelector('ul li') // 첫번째 li만
querySelectorAll('ul li') // 모든 li

querySelector('.link-content') // 앞에 .쓰는것 잊지말자. 선택자를 넣는것이지 문자열을 넣는게 아님
querySelector('* > .link-content') // css에서는 * 를 생략해도 되지만 여기서는 명시해줘야함. (* > 는 직계자손을 찾는다.)
```

- `document.getElementsByClassName`
탐색 스크립트이다. 
getElementByID의 경우 ID가 부여된 단 하나의 요소만을 탐색할 뿐이며 getElementsByTagName의 경우 동일 태그의 모든 요소를 반환한다. 만일 임의의 이름이 부여된 특정 그룹을 탐색하고자 할 경우 이 두가지만으로는 한번에 만족시킬 수 없다. getElementsByClassName 은 그 이름에서도 알 수 있듯이 className 이 부여된 요소(그룹)을 반환한다.

- 페이지에 다음과 같이 동일한 class가 부여된 div 요소가 정의되어 있다면,
```html
<div class="myDivClass">First Div</div>
<div class="myDivClass">Second Div</div>
```
- 다음과 같이 class 명으로 div 요소 그룹을 탐색할 수 있다
```js
var element1 = document.getElementsByClassName("myDivClass");    
    
for(var i = 0; i < element1.length; i++){
   alert(element1[i].nodeName);  
}
```


## 정규표현식
- 참고 : <https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/RegExp>
```js
/pattern/flags         //문자표기방식
new RegExp(pattern[, flags])       //생성자로 만들때
```
- `pattern` : 정규식(regular expression)을 나타내는 문자
- `flags`
  - g : global match; 일치하는 첫 번째 문자에서 멈추지 않고 전체에서 일치하는 모든 문자를 검색합니다.
  - i : ignore case(대소문자를 구별하지 않습니다.)
  - m : multiline; 시작 혹은 끝 문자 탐색(^ and $)이 다중행에 적용되도록 합니다.  (예로,  \n 혹은 \r로 개행된 각각의 라인 시작 혹은 끝 뿐만 아니라, 전체 입력 문자의 시작 혹은 끝에서 일치합니다.
```js
[href^=".pdf"]{} // => 시작 start
[href$=".pdf"]{} // => 끝 end
[href*=".pdf"]{} // => 어디든 있는거
\s // => white space character empty

x|y // => x or y
```
- 예시
  - link-content 의 앞에 공백이 오거나
  - link-content 의 뒤에 공백이 오거나
  - link-content 의 양쪽에 공백이 오거나
```js
var keyword = 'link-content';
var match = new RegExp('/(^|\s) + match + ($|\s)/')
/(^|\s)link-content($|\s)/.test('link-content external') // true
```



```js
// IE 9+ 에서만 지원되는 신 기술
    // function classes(name, context) {
    //   return (context || document).getElementsByClassName(name);
    // }

    // IE 8- 에서도 호환되는 크로스 브라우징 유틸리티 메서드
    var classAll = function(){
    var _classAll = null;
    // 조건 처리
    // el.getElementsByClassName 지원하는가?
    // 'getElementsByClassName' in Element.prototype
    // 상황에 맞는 함수를 선별하여 할당한 후, 내보내자
    if ( 'getElementsByClassNames' in Element.prototype ) { // 최신버전
      _classAll = function(name, context) {
        // name 문자열(class 속성명)
        validateError(name, '!string', '첫번째 전달인자는 문자열을 전달해야 합니다.');
        // context = context || document.body;
        // validateElementNode(context);
        context = context || document;
        if ( context !== document && !isElementNode(context) ) { throw '두번째 인자로 요소노드를 전달해 주세요'; }
        return context.getElementsByClassName(name);
        // context 상위 객체(요소노드, document 객체)
      };
    } else { // 구형버전
      _classAll = function(name, context) {
        // context 객체 내부의 요소 class 속성 값이
        // name 값과 일치하는 요소들의 집합을 반환한다.
        // --------------------------------------------
        // 전달인자 유효성 검사
        validateError(name, '!string', '첫번째 전달인자는 문자열이어야 합니다.');
        // context 초기값 설정
        context = context || document; // document.body
        // context 객체 유효성 검사
        if ( context !== document && !isElementNode(context) ) { throw '두번째 인자로 요소노드를 전달해 주세요'; }
        // --------------------------------------------
        // context 내부에서 모든 요소를 찾아라!
        var _alls = tagAll('*', context);
        var _matched = [];
        var match = new RegExp('(^|\\s)' + name + '($|\\s)');
        for ( var i=0, l=_alls.length; i<l; ++i ) {
          var _el = _alls.item(i);
          // case 1
          // context(부모) 객체 내부의 자식(el)을 하나 하나 검증
          // 검증 내용: name 값하고 el의 className 하고 일치하는지
          // if ( name !== '' && name === _el.className ) {
            // 일치한다면 수집하여 반환
            // _matched.push(_el);
          // }

          // case 2
          // name 을 변수로 하는 정규 표현식을 작성
          // var match = new RegExp('(^|\\s)' + name + '($|\\s)'); // 위로 올려줌
          // 정규표현식 객체의 test() 메서드를 사용해서 문자가 일치하는지 검증
          // 검증 값이 참이면, 수집한다.
          if ( match.test(_el.className) ) {
            _matched.push(_el);
          }
        }
        return _matched;
      };
    }
    return _classAll;
  }();
```

## 이미지 링크 사이트
- <https://placeimg.com/>
- <https://unsplash.it/>


## 'this' 에 대한 조금 더 괜찮은 예제
- 참고
 <http://resoneit.blogspot.kr/2014/01/this.html>
 <https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this>
 <http://webframeworks.kr/tutorials/translate/explanation-of-this-in-javascript-1/>


### this 정의
- 전역 컨텍스트 : 전역에서(어떤 함수 외부) this는 전역 객체를 나타낸다. 웹브라우저에서 전역객체는 window
- 함수 컨텍스트 : 함수내부에서 this는 호출한 방법에 의해 좌우된다.

### 각 상황에 따라 this가 가리키는 것
1. 기본적으로 global 객체이다. (window)
- strict mode가 아닐 때 this의 값은 항상 window
```js
function f1(){
  return this;
}
f1() === window; // 전역 객체

function sum(a, b) {
   console.log(this === window); // => true
   this.myNumber = 20; // 전역 객체에 'myNumber'라는 속성을 추가
   return a + b;
}
```
- strict mode일 때 undefined ( 실행 컨텍스트에 들어갈 때 할당되어 유지. 만약 정의되지 않았을 경우 undefined. null, 숫자, 문자값 등으로 설정 가능. 엄격모드는 내부 함수에서도 적용된다.)
```js
function f2(){
  "use strict"; // strict mode
  return this;
}
f2() === undefined;
//  f2가 어떠한 기본(예. f2())도 제공하지 않고 호출했다. 이 기능은 strict mode를 지원하기 위해 시작했을 때 일부 브라우저에서 구현되지 않았다. 결과적으로, window 객체를 잘못 반환했다.
```
```js
// 내부 함수에서의 this
var numbers = {
   numberA: 5,
   numberB: 10,
   sum: function() {
     console.log(this === numbers); // => true
     function calculate() {
       // this는 window, 엄격 모드였으면 undefined
       console.log(this === numbers); // => false
       return this.numberA + this.numberB;
     }
     return calculate();
   }
};
numbers.sum(); // NaN, 엄격 모드였으면 TypeError
```

2. new연산자(생성자)로 생성된 function 영역에서 this는 새롭게 생성된 객체 그 자신이다.
```js
function F (v) {
  this.val = v;
}
var f = new F(“Woohoo!”);
console.log(f.val); // Woohoo!
console.log(val); // ReferenceError
```
3. 객체의 prototype 체인에서 this는 호출된 객체이다.
```js
var o = {f:function(){ return this.a + this.b; }};
var p = Object.create(o);
p.a = 1;
p.b = 4;

console.log(p.f()); // 5
```

4. 메소드 실행에서의 this는 메소드를 소유하고 있는 객체다.(객체 내에 있는 메소드를 실행할 때, 여기서의 this는 자기자신)
```js
var calc = {
  num: 0,
  increment: function() {
    console.log(this === calc); // => true
    this.num += 1;
    return this.num;
  }
};
// 메소드 실행. 여기서의 this는 calc.
calc.increment(); // => 1
calc.increment(); // => 2
```

5. getter와 setter에서의 this는 get 또는 set 되는 속성 객체다.
```js
function modulus(){
  return Math.sqrt(this.re * this.re + this.im * this.im);
}

var o = {
  re: 1,
  im: -1,
  get phase(){
    return Math.atan2(this.im, this.re);
  }
};

Object.defineProperty(o, 'modulus', {
    get: modulus, enumerable:true, configurable:true});

console.log(o.phase, o.modulus); // logs -0.78 1.4142
```

6. call, apply, bind 메서드로 this를 특정한 객체와 연결할 수 있다.
```js
var add = function (x, y) {
      this.val = x + y;
    },
    obj = {
      val: 0
    };
add.apply(obj, [2, 8]);
console.log(obj.val); // 10
add.call(obj, 2, 8);
console.log(obj.val); // 10

function f(){
  return this.a;
}

var g = f.bind({a:"azerty"});
console.log(g()); // azerty

var o = {a:37, f:f, g:g};
console.log(o.f(), o.g()); // 37, azerty
```

7. DOM 이벤트 핸들러로 사용되는 함수에서 this는 이벤트가 발생한 엘리먼트다.
```js
// 리스너로서 호출될 때, 관련된 엘리먼트를 파랗게 만든다.
function bluify(e){
  // 항상 true
  console.log(this === e.currentTarget); 
  // currentTarget 과 target 이 같은 객체일 때 true
  console.log(this === e.target);
  this.style.backgroundColor = '#A5D9F3';
}

// document의 모든 엘리먼트의 목록을 얻는다.
var elements = document.getElementsByTagName('*');

// 클릭 리스너로 bluify를 추가하여서 엘리먼트를 클릭하면, 그 엘리먼트는 파랗게 된다.
for(var i=0 ; i<elements.length ; i++){
  elements[i].addEventListener('click', bluify, false);
}
```