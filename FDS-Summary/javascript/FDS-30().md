FDS-30-
========


## insertBefore


## lang="en"을 써주는 이유
```html
  <div class="wrapper">
    <p lang="en">lorem is...</p>
  </div>
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
- 프레임워크로 인해 과거로 돌아간다
- 무조건 전역함수여야 한다. -> 글로벌 오브젝트를 사용해서 밖으로 노출 시켜준다.
- 표현식으로 써준다.(클로저같은 일을 해준다.)

```html
<button onclick="changePosition()" type="button" class="button is-change-position">위치변경</button>
```
```js
function methodTow(){
   var wrapper_p = $.selector('.wrapper p');
   var target = $.selector('.wrapper .target');

   global.changePosition = function(){
      $.parent(wrapper_p).insertBefore(target, wrapper_p);
   };
}
methodTwo();
```
- 그런데 이벤트를 해제할 수 가 없다.
- 왜냐면 아까는 자바스크립트에 문서 객체를 참조해와서 null을 줬는데, 지금은 문서 내에 있잖아.
- 디스 에이블, 이벤트 제거
- 버튼을 더이상 클릭 할 수 없게만들기
- 함수를 실행시킨 주체 (this)는 누구냐
```html
<button onclick="changePosition(this)" type="button" class="button is-change-position">위치변경</button>
```
온클릭 속성값 안에 함수 식은 들어갈 수 있다. 문은 안됨.
this에 접근할 수 있게 되었다.
```js
function methodTow(){
   var wrapper_p = $.selector('.wrapper p');
   var target = $.selector('.wrapper .target');

   global.changePosition = function(button){
      button.setAttribute('disabled','disabled'); // 지금 html은 disabled하나만 써줘도 되지만, xhtml은 disabled="disabled써줘야해서
      button.removeAttribute('onclick'); // 속성 지우기
      $.parent(wrapper_p).insertBefore(target, wrapper_p);
   };
}
methodTwo();
```

```js
    // 방법 1. .wrapper를 찾아서...
    function methodOne() {
      var wrapper = $.selector('.wrapper');
      var new_node = $.createEl('h1', 'insertBefore');
      new_node.setAttribute('lang', 'en');
      new_node.setAttribute('class', 'wrapper-headline');
      // 문서의 특정 요소노드에 마운트(Mount)되지 않은 상태
      console.log('new_node:', new_node);
      // ~ 앞에 삽입해보자.
      // 부모노드.insertBefore(삽입노드, 부모노드를_통해_찾은_자식노드)
      // 이벤트가 요구된다면
      wrapper.onmouseover = function() {
        // 문서의 특정 요소노드에 마운트(Mount)된 상태
        this.insertBefore(new_node, $.selector('p', this));
        // 이벤트의 제거
        this.onmouseover = null;
      };
    }
    // methodOne();
```
```js
    // 방법 2. .wrapper p 요소를 찾아서...
    function methodTwo(){
      // 문서에서 대상 찾기
      var wrapper_p = $.selector('.wrapper p');
      var target = $.selector('.wrapper .target');
      // 전역에 changePosition() 함수를 공개
      global.changePosition = function(button) {
        // console.log('this:', this);
        // console.log('button:', button);
        button.setAttribute('disabled', 'disabled');
        button.removeAttribute('onclick');
        // console.log('changePosition() 함수 실행');
        // 상대적으로 insertBefore() 메서드 사용하기
        // 목표노드.부모노드.insertBefore(삽입노드,목표노드);
        $.parent(wrapper_p).insertBefore(target, wrapper_p);
      };
    }
    methodTwo();
```

## apply, call, bind 복습



```js
    var mount = $.selector('.mount');
    var list_contents = '아메리카노 카페라떼 차이티라떼 모카카푸치노'.split(' ');
    // 템플릿(TEMPLATE) 코드
    // <ul class="list">
    //   <li class="list-item">content</li>
    // </ul>

    function innerHTMLDemo() {
      
    }

    // function replaceChildDemo() {
    //   // data(list-content)를 순환 처리 해서 동적으로 HTML 코드로 생성
    //   // html 코드를 조합하기 위한 기본 문자열을 참조하는 변수 정의
    //   var list_html = '<ul class="list">';

    //   // list_content 데이터 반복 처리
    //   for ( var content, i=0, l=list_content.length; i<l; ++i ) {
    //     content = list_contents[i];
    //     list_html += '<li class="list-item">' + content + '</li>';
    //   }
    //   // 순환 종료 후에 마무리
    //   list_html += '</ul>';
    //   console.log(list_html);
    //   // .innerHTML : (속성) html 코드로 바뀐다. 자기를 비 포함하고
    //   // 동적으로 HTML 코드를 mount 요소의 내부 코드로 대체 연결
    //   mount.innerHTML = list_html;
    // }

    function replaceChildDemo() {
      
    }
    replaceChildDemo();
```


## `<li tabindex="0" class="list-item">`

## 정규표현식

var test_reg = new RegExp('(^|\\s) + + '(&|\\s)');