FDS-30-요소추가/제거 실습
========
 


## lang="en"을 써주는 이유
- 기본 설정된 언어와 다른 언어가 중간에 들어올 때 발음을 제대로 읽어줌
- 한글폰트와 영어폰트를 다르게 주고 싶을 때?
```html
<html lnag="ko"
  <div class="wrapper">
    <p lang="en">lorem is...</p>
  </div>
</html>
```

## OOCSS(Object Oriented CSS)
- 참고 : <https://mytory.net/archives/8949>
- 객체 지향 css
- 코드 재사용성을 높이고 더 빠르고 효율적이며 추가하기 쉽고 유지보수하기 용이한 스타일시트를 만드는 것
- 겉모양(skin)에서 골격(structure)을 분리하기
- 컨테이너와 콘텐츠를 분리하기
  - 계층적 선택자를 피하라. (예컨대, .sidebar h3 같은 것을 사용하지 말라.)
  - 자바스크립트 이벤트를 거는 ID에 스타일을 입히지 말라.
  - 스타일시트 클래스에 HTML 태그를 적지 말라. (예컨대 div.header, h1.title)
  - 정말 드문 경우를 외에는 !important를 사용하지 말라.
  - CSS Lint를 이용해서 CSS를 검사하라. (옵션과 오류 종류를 익혀라.)
  - CSS 그리드를 사용하라.

## 겸손한 자바스크립트
- 참고: <http://www.clearboth.org/43_the_principles_of_unobtrusive_javascript/>
### 정의
- 모든 브라우저가 자바스크립트를 지원하지 않는다. => 자바스크립트를 없애도 사이트를 이용할 수 있어야 한다.
- 모든 브라우저들은 똑같이 동작하지 않는다. => 크로스 브라우징, 호환성, 다양한 기기 지원
- 다른 모든 이들이 내 코드를 이해할 수는 없다. => 코드를 깔끔하게, 주석을 많이 달기
### 구조(html)와 행동(javascript)의 분리
- HTML 파일은 자바스크립트 코드를 포함하면 안된다. => HTML에는 내장된 스크립트와 이벤트 핸들러만 넣을 수 있다.

## 인라인 이벤트 (구형방식)
- 프레임워크로 인해 과거로 돌아간다.
- 그런데 이벤트와 연결된 함수는 무조건 전역함수여야 한다. -> 글로벌 오브젝트를 사용해서 밖으로 노출 시켜준다.
- 표현식으로 써준다.(클로저같은 일을 해준다.)
```html
<button onclick="changePosition()" type="button" class="button is-change-position">위치변경</button>
```
```js
function methodTow(){
   var wrapper_p = $.selector('.wrapper p');
   var target = $.selector('.wrapper .target');

   global.changePosition = function(){ // 글로벌 오브젝트를 사용해서 밖으로 노출, 표현식 사용
      $.parent(wrapper_p).insertBefore(target, wrapper_p);
   };
}
methodTwo();
```
### 이벤트 삭제
- 버튼을 더이상 클릭 할 수 없게만들어야 하는데,
- 이벤트를 해제할 수 가 없다.
- 왜냐면 분리된 자바스크립트에는 문서 객체를 참조해와서 null을 주면 되는데, 지금은 문서 내에 있잖아.
- disabled, 이벤트 제거
- 함수를 실행시킨 주체 (this)는 누구냐 => button
- `disabled`
- `removeAttribute`
```html
<button onclick="changePosition(this)" type="button" class="button is-change-position">위치변경</button>
<!-- onclick 속성값 안에 함수 식은 들어갈 수 있다. 문은 안됨.-->
<!-- this에 접근할 수 있게 되었다.-->
```
```js
function methodTow(){
   var wrapper_p = $.selector('.wrapper p');
   var target = $.selector('.wrapper .target');

   global.changePosition = function(button){
      button.setAttribute('disabled','disabled'); // 지금 html은 disabled하나만 써줘도 되지만, xhtml은 disabled="disabled"로 써줘야 해서
      button.removeAttribute('onclick'); // 속성 지우기
      $.parent(wrapper_p).insertBefore(target, wrapper_p);
   };
}
methodTwo();
```

## insertBefore(target)
- target : 선택자(selector), 요소(element), HTML 문자열..
### insertBefore을 이용한 utils 함수
```js
// target요소 앞에 insert요소를 삽입하는 함수
var insertBefore = function(insert, target) {
  validateElementNode(insert);
  validateElementNode(target);
  parent(target).insertBefore(insert, target);
  return insert;
};
var before = function(target, insert) {
  return insertBefore(insert, target);
};
var prependChild = function(parent, child) {
  validateElementNode(parent);
  validateElementNode(child);
  var target = firstChild(parent);
  return target ? insertBefore(child, target) : appendChild(parent, child);
  // 내 밑으로 첫번째 자식(target)이 있으면 target요소 앞에 child요소를 삽입하고 target이 없으면 child를 자식요소로 만들어라.
};
// target요소 뒤에 insert요소를 삽입하는 함수
var insertAfter = function(insert, target) {
  var next = nextSibling(target);
  return next ?  insertBefore(insert, next) : appendChild(parent(target), insert);
};
var after = function(target, insert) {
  return insertAfter(insert, target);
};
```

## 새로운 요소 삽입하기
`<h1 lang="en" class="wrapper-headline">insertBefore</h1>` 요소 삽입하기
```html
<div class="wrapper">
  <button onclick="changePosition(this)" type="button" class="button is-change-position">위치 변경</button>
  
  <!--.wrapper 내부에 p 요소를 소유하고 있다.-->
  <p lang="en">Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
  <ul class="target" lang="en">
    <li><a href="">content-01</a></li>
    <li><a href="">content-02</a></li>
  </ul>
</div>
```
### 방법 1. 부모를 통해 찾은 자식노드 앞에 삽입하기
- ~ 앞에 삽입해보자.
- 부모노드.insertBefore(삽입노드, 부모노드를_통해_찾은_자식노드)
```js
    function methodOne() {
      var wrapper = $.selector('.wrapper');
      var new_node = $.createEl('h1', 'insertBefore'); 
      new_node.setAttribute('lang', 'en');
      new_node.setAttribute('class', 'wrapper-headline');
      // 문서의 특정 요소노드에 마운트(Mount)되지 않은 상태
      console.log('new_node:', new_node);
   
      // 이벤트가 요구된다면
      wrapper.onmouseover = function() {
        // 문서의 특정 요소노드에 마운트(Mount)된 상태
        this.insertBefore(new_node, $.selector('p', this));
        // 이벤트의 제거
        this.onmouseover = null;
      };
    }
    methodOne();
```
### 방법 2.대상노드를 찾아서 삽입하기
- 상대적으로 insertBefore() 메서드 사용하기
- 목표노드.부모노드.insertBefore(삽입노드,목표노드);
```js
    function methodTwo(){
      // 문서에서 대상 찾기
      var wrapper_p = $.selector('.wrapper p');
      var target = $.selector('.wrapper .target');
      // 전역에 changePosition() 함수를 공개
      global.changePosition = function(button) {
        $.parent(wrapper_p).insertBefore(target, wrapper_p);
      };
    }
    methodTwo();
```
## removeChild
- 부모노드.removeChild(자식노드)
### removeChild를 이용한 utils 함수
```js
var removeChild = function(child) {
  validateElementNode(child);
  return parent(child).removeChild(child);
};
var replaceChild = function(replace, target) {
  validateElementNode(target);
  return parent(target).replaceChild(replace, target);
};
```

## class속성 추가/제거 utils 함수
```js
// class속성에 name이라는 이름을 가진 클래스가 있는지 검사하는 함수
var hasClass = function(el, name) {
  validateElementNode(el);
  validateError(name, '!string');
  var el_classes = el.getAttribute('class');
  var reg = new RegExp('(^|\\s)' + name + '($|\\s)'); // name 앞에, 뒤에, 양쪽에 공백이 있다.
  return reg.test(el_classes); // true | false
};
var addClass = function(el, name) {
  if ( !hasClass(el, name) ) { // name이라는 클래스가 없으면
    var new_value = (el.getAttribute('class') || '') + ' ' + name; // 원래 클래스를 가져와서 빈 문자열에 name을 더해줘라.
    el.setAttribute('class', new_value.trim());
  }
  return el;
};
var removeClass = function(el, name) {
  if ( !name ) {
    validateElementNode(el);
    el.removeAttribute('class');
  } else {
    if ( hasClass(el, name) ) {
      var reg = new RegExp(name);
      var new_value = el.getAttribute('class').replace(reg, '');
      el.setAttribute('class', new_value.trim());
    }
  }
  return el;
}; 
var toggleClass = function(el, name) {
  return hasClass(el, name) ? removeClass(el, name) : addClass(el, name);
};
var radioClass = function(el, name) {
  validateElementNode(el);
  validateError(name, '!string');
  var old_active = query('.'+name, parent(el));
  old_active && removeClass(old_active, name);
  return addClass(el, name);
};
```


## bind 응용
### bind를 이용해서 this 바꿔주기
```js
function bindEvents() {
  var wrapper = $.selector('.input-field-wrapper');
  var button = $.selector('button', wrapper);
  button.onclick = replaceListItem.bind(button, wrapper);
}
```
### bind를 이용해서 즉시실행되지 않게 만들기
```js
function removeChildDemo() {
  global.setTimeout(afterTimeRemove, 2200); // 2.2초 뒤 실행
}
removeChildDemo();

function afterTimeRemove() {
  var removed_el = $.selector('.target');
  removed_el = $.removeChild(removed_el);
  // global.setTimeout(function(){
  //   afterTimeAndAttach(removed_child);
  // }, 3000);

  global.setTimeout(afterTimeAndAttach.bind(removed_el), 3000); 
  // 3초뒤 실행 .apply, .call 과달리 즉시실행하지 않고 뒤에 인자로 들어온만큼 늦게 실행해줌.
}
function afterTimeAndAttach() {
  // console.log(this); // removed_child 
  $.insertAfter(this, $.selector('.prepend-demo :first-child'));
}
```


## innerHTML
-  HTML구문의 하위 노드들을 가져오거나, 설정한다.
```js
var mount = $.selector('.mount');
var list_contents = '아메리카노 카페라떼 차이티라떼 모카카푸치노'.split(' ');
// 템플릿(TEMPLATE) 코드
// <ul class="list">
//   <li class="list-item">content</li>
// </ul>

function replaceChildDemo() {
  // data(list-content)를 순환 처리 해서 동적으로 HTML 코드로 생성
  // html 코드를 조합하기 위한 기본 문자열을 참조하는 변수 정의
  var list_html = '<ul class="list">';
  // list_content 데이터 반복 처리
  for ( var content, i=0, l=list_content.length; i<l; ++i ) {
    content = list_contents[i];
    list_html += '<li class="list-item">' + content + '</li>';
  }
  // 순환 종료 후에 마무리
  list_html += '</ul>';
  console.log(list_html);
  // .innerHTML : (속성) html 코드로 바뀐다. 자기를 비 포함하고
  // 동적으로 HTML 코드를 mount 요소의 내부 코드로 대체 연결
  mount.innerHTML = list_html;
}
replaceChildDemo();
```

## tabindex
- 참고: <http://mygumi.tistory.com/53>
- 키보드 접근성에 근접한 속성
- 어떤 엘리먼트에 키보드 포커스를 주는 방법
  - 0 값 - tabindex="0" : 포커스 기능이 없는 엘리먼트에게 포커스를 줄 수 있다. 
  - 양수 - tabindex="1~32768" : 탭 순서를 지정 (숫자가 낮을수록 우선순위)
  - 음수 - tabindex="-1" : 포커스 기능이 있는 엘리먼트에게 포커스를 없앨 수 있다.

```html
<li tabindex="0" class="list-item">
<!-- li 요소는 키보드 포커스 기능이 없지만 tabindex="0"을 주어서 포커스를 줬다. -->
```