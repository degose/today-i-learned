FDS-33-노드복사/클래스속성/DOM삽입
========

## cloneNode
- `.cloneNode([deep])`
- deep : (true || false) True면 이 노드 아래에 있는 전체 트리의 복제. False 인 경우, 이 노드 및 해당 특성에만 복제
- 복제된 새로운 노드를 반환

## forEach
- 참고: <https://msdn.microsoft.com/ko-kr/library/ff679980(v=vs.94).aspx>
- `array1.forEach(callbackfn[, thisArg])`
- 배열에 있는 각 요소에 대해 한 번씩 오름차순 인덱스 순서로 callbackfn 함수를 호출. 
- 배열 개체 외에도 forEach 메서드를 사용하면 length 속성을 포함하는 개체와 숫자로 인덱싱된 속성 이름을 포함하는 모든 개체에서 사용 가능
- callbackfn
  - `function callbackfn(value, index, array1)`
  - 최대 3개의 인수를 받아들이는 함수 forEach는 배열에 있는 각 요소마다 한 번씩 callbackfn 함수를 호출
  - value : 배열요소의 값(key)
  - index : 배열요소의 숫자 인덱스
  - array1 : 요소가 포함된 배열 개체
- thisArg
  - this 키워드가 callbackfn 함수에서 참조할 수 있는 개체. thisArg가 생략되면 undefined가 this 값으로 사용
- 특징
  - ES5(2009) IE 8 이하는 지원하지 않는다. -> es5shim.js 라이브러리를 쓴다면 가능
  - vue.js도 IE 8 이하로 지원할 수 없다.
  - length값을 알지 못해도 알아서 출력
  - for문과의 차이점: for문은 break 를 만나면 멈추지만 forEach문은 멈출 수 없다.
  - for문은 증가 값을 2, 3 등 설정 할 수 있지만 forEach문은 1씩만 증가
```js
[3,7,0,101].forEach(function(item, index, arr){
  console.log(arguments);
});
```
- this 키워드로 참조할 수 있는 개체를 지정하는 thisArg 인수를 사용하는 방법
```js
// Define the object that contains the callback function.
var obj = {
  showResults: function(value, index) {
    // Call calcSquare by using the this value.
    var squared = this.calcSquare(value);

    document.write("value: " + value);
    document.write(" index: " + index);
    document.write(" squared: " + squared);
    document.write("<br />");
  },
  calcSquare: function(x) { return x * x }
};

// Define an array.
var numbers = [5, 6];

// Call the showResults callback function for each array element.
// The obj is the this value within the 
// callback function.
numbers.forEach(obj.showResults, obj);

// Embed the callback function in the forEach statement.
// The obj argument is the this value within the obj object.
// The output is the same as for the previous statement.
numbers.forEach(function(value, index) { this.showResults(value, index) }, obj);

// Output:
//  value: 5 index: 0 squared: 25
//  value: 6 index: 1 squared: 36
//  value: 5 index: 0 squared: 25
//  value: 6 index: 1 squared: 36
```

### 콜백함수 복습


### 제이쿼리에서 forEach
- 순서가 달라

### forEach문을 이용한 utils 함수
- Array.prototype.forEach() 인스턴스 메서드
```js
  var forEach = Array.prototype.forEach;
  function each(o,callback) {
    // 배열, 객체를 순환하여 전달된 콜백함수를 처리
    // 전달된 o의 유형 파악

    // callback이 함수 유형인지 검증
    validateError(callback, '!function');

    // 조건분기
    // 유사배열 객체: 객체가 아니면서 .length 속성을 가졌다면 배열로 변경
    if(!isObject(o) && o.length) { o === makeArray(o);}
    // 1. 배열 or 유사배열
    // if(isArray(o) || type(o) === 'nodelist') {
    if(isArray(o)) {
      // 1.1 IE 8- : for문
      if(!forEach) {
        for ( var item, i=0, l=o.length; i<l; ++i) {
          item = o[i]; 
          // callback함수 처리하자, 유사배열도 처리하자
          callback.call(o, item, i, o); // this는 o
        }
      }
      // 1.2 IE 9+ : forEach문
      else {
        o.forEach(callback);
      }
    }
    // 2. 객체
    if(isObject(o)) {
      // 객체의 속성을 순환 처리
      for (var prop in o) {
        if ( o.hasOwnProperty(prop)) {
          var value = o[prop];
          callback(prop, value, o);
        }
        o.hasOwnProperty(prop) && callback(prop, o[prop], o);
      }
    }

```
- 어떻게 쓸건지?
```js
each(['a','b']), function (item, index, data) {
  
};
each({
  color: '#333',
  backgroundColor: '#fff'
}, function (key, value, o) {

  })
```




## event
```js
function(event)
link.onclick = event | global

var forEach = Array.prototype.forEach;
forEach.call(gnb_links, function (link) {
  link.onclick = function () {
    // e.preventDefault();
    console.log(this);
    return false;
  };
});

// 구형방식
return false;
```

## 바인딩
```js
  // #gnb 내부의 a 요소에 이벤트 바인딩
  var gnb_links = $.selectorAll('a', gnb);
```


## 클래스 속성 제어
- 속성 추가 제거 소유 토글
- `.classList`
  - `.contains()`: 포함되어 있느냐(hasClass)
  - `.add()`: 
  - `.remove()`: 
  - `.toggle()`
  - `.values()`
  - `.entries()`
- utils 함수에서 hasClass를 보완
  - IE 9- 를 위하여
  ```js
  var hasClass = function(el, name) {
  validateElementNode(el);
  validateError(name, '!string');
  var el_classes = el.getAttribute('class');
  var reg = new RegExp('(^|\\s)' + name + '($|\\s)');
  return reg.test(el_classes);
  };
  ```
  ```js
  var hasClass = function () {
  if ('classList' in Element.prototype) {
    return function (el, name) {
      validateElementNode(el);
      validateError(name, '!string');
      return el.classList.contains(name);
    };
  } else {
    return function(el, name) {
      validateElementNode(el);
      validateError(name, '!string');
      var el_classes = el.getAttribute('class');
      var reg = new RegExp('(^|\\s)' + name + '($|\\s)');
      return reg.test(el_classes);
    }
  }
  }();
  ```

## DOM 삽입
- `.innerHTML`
  - getter / setter
  - [GETTER] Node.innerHTML
  - [SETTER] Node.innerHTML = 'HTML Code';
  - 기존에 존재하던 모든 요소는 사라진다.(갈아 끼워짐)
  - 버튼을 누르면 textarea에 써 넣은 html코드로 교체되는 프로그램
  - .button.is-change-html-code <button> 요소를 클릭하면 #user-html-code <textarea> 요소의 값(value) -> HTML 코드를 .html-wrapper 내부에 적용하여 화면을 업데이트 하시오.
  ```html
  <body>

    <button type="button" class="button is-change-html-code">HTML 교체</button>
    <p>
      <textarea
        id="user-html-code"
        class="html-wrapper"
        cols="30"
        rows="10"
        placeholder="추가하고자 하는 HTML 코드를 작성하세요."></textarea>
    </p>

    <div class="html-wrapper">
      <dl>
        <dt>일시</dt>
        <dd>2017년 6월 27일</dd>
        <dt>요일</dt>
        <dd>화</dd>
      </dl>
    </div>

  </body>
  ```
  ```js
  // .button.is-change-html-code <button> 요소를 클릭하면 
  var change_btn = $.selector('.button.is-change-html-code');
  var textarea = $.selector('#user-html-code');
  // 이벤트 바인딩

  change_btn.onclick = render;

  // 사람이 읽기 용이한(Readable) 키코드 객체
  var keyboards = {
    enter: 13
  }

  // 키보드 이벤트 감지 및 처리
  textarea.onkeyup = function (e) {
    var key = e.keyCode || e.which;
    console.log('key:', key); // Enter(13)
    if (key === keyboards.enter) {
      render();
    }
  }
  // render 핸들러(함수)
  function render() {
    var html_code = textarea.value;
    // #user-html-code <textarea> 요소의 값(value) -> HTML 코드를 
    // .html-wrapper 내부에 적용하여 화면을 업데이트 하시오.
    $.selector('div.html-wrapper').innerHTML = html_code;
  }
  ```

- 크로스 브라우징
  - prepend()
  - append()
  - before()
  - after()

- `.insertAdjacentHTML(position, html_code)`
  - position
  - before, after
  - begin, end
  ```js
  var target = $.selector('.insert-adjacent-html .target');
  target.insertAdjacentHTML('beforebegin', '<h2 class="beforebegin">beforebegin</h2>');
  target.insertAdjacentHTML('afterbegin', '<strong class="afterbegin">afterbegin</strong>');
  target.insertAdjacentHTML('beforeend', '<strong class="beforeend">beforeend</strong>');
  target.insertAdjacentHTML('afterend', '<h2 class="afterend">afterend</h2>');
  ```
- `.insertAdjacentElement()`
  - Element.insertAdjacentElement(position, element)
  - element: 요소노드 값을 입력한다.
  - insertAdjacentHTML 과 같은 포지션 값을 가진다.
  - IE 9+
  ```js
  target.insertAdjacentElement('beforebegin', $.createEl('h2','beforebegin'));
  target.insertAdjacentElement('afterbegin', $.createEl('strong','afterbegin'));
  target.insertAdjacentElement('beforeend', $.createEl('strong','beforeend'));
  target.insertAdjacentElement('afterend', $.createEl('h2','afterend'));
  ```
- `.insertAdjacentText()`
  - Element.insertAdjacentText(position, element)
  - element: Text 값을 입력한다.
  - insertAdjacentHTML 과 같은 포지션 값을 가진다.
  - IE 9+
  ```js
  target.insertAdjacentText('beforebegin', 'beforebegin');
  target.insertAdjacentText('afterbegin', 'afterbegin');
  target.insertAdjacentText('beforeend', 'beforeend');
  target.insertAdjacentText('afterend', 'afterend');
  ```
  ```js
  beforeBtn.addEventListener('click', function() {
  para.insertAdjacentText('afterbegin',textInput.value);
  });

  afterBtn.addEventListener('click', function() {
  para.insertAdjacentText('beforeend',textInput.value);
  });
  ```


## 실습
- 참고: <http://emailregex.com/>

## e.target
- 참고: <https://www.w3schools.com/jsref/event_target.asp>
- 참고: <http://krespo.net/88>

## HTMLElement.dataset
- 참고: <https://developer.mozilla.org/fr/docs/Web/API/HTMLElement/dataset>
- 데이터 접두사 제어 메소드
- data-  로 시작하는 값을 제어할수 있다.
- DOMStringmap
- 참고: <https://developer.mozilla.org/en-US/docs/Web/API/DOMStringMap> 
```javascript
target.setAttribute('data-tag-name',target.localName);
target.setAttribute('data-node-type',target.nodeType);
target.setAttribute('data-has-class',target.hasAttribute('class'));
console.log('target.dataset',target.cataset);
```

## 네이밍관례 종류 (Naming convention)
- TitleCase : `TitleCaseNaming` (UpperCamelCase,PascalCaseNaming) 첫 단어를 대문자로 시작하는 표기법
- CamelCase : `camelCaseNaming` (lowerCamelCase) 각 단어의 첫문자를 대문자로 표기하고 붙여쓰되, 맨처음 문자는 소문자로 표기
- SnakeCase : `snake_case_naming` 단어를 밑줄문자(_)로 구분하는 표기법
- KebabCAse : `kebab-case-naming` 소문자에 dash(-) 조합
  - html,css에서는 class명으로 케밥케이스를 많이 쓰는데, 자바스크립트에서 하이픈은 빼기(-)로 인식할 수 있어서
  - 객체의 key 값을 케밥케이스로 할때에는 따옴표로 감싸줘야 한다.
  ```html
  <div class="html-wrapper">
    작성한 HTML 코드가 이 곳에 동적으로 처리됩니다. :-)
  </div>
  ```
  ```js
  // #user-html-code <textarea> 요소의 값(value) -> HTML 코드를
  // .html-wrapper 내부에 적용하여 화면을 업데이트 하시오.
  $.selector('div.html-wrapper').innerHTML = html_code;
  ```
- 참고: <http://www.w3im.com/ko/js/js_conventions.html>


## Focus Element 종류
- 참고: <https://goo.gl/xWM8U4>
- href 속성을 가진 엘리먼트
  - a        
  - area     
  - button   
  - input    
  - textarea 
  - object   
  - select 
