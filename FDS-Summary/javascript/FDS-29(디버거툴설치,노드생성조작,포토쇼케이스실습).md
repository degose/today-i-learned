FDS-29-디버거툴설치,노드 생성조작,포토쇼케이스실습
========


## debugger for chrome 설치
- 구성추가 -> name에 이름정해주고 -> workspace에 경로 잘 적어주면 끝
```
{
    "version": "0.1.0",
    "configurations": [
      {
        "name": "Day13",
        "type": "chrome",
        "request": "launch",
        "sourceMaps": false,
        "file": "${workspaceRoot}/DAY13/javascript.study.html"
      }
    ]
}
```


## 노드 생성
  html문서를 자바스크립트로 생성할 수 있다.
- `document.createElement('element')` : 지정된 태그이름을 가지는 엘리먼트 생성
- `document.createAttribute('attribute')` : 지정된 속성이름을 가지는 속성 생성
- `document.createTextNode('text')` : 지정된 텍스트의 콘텐츠 생성
```js
// 동적으로 요소노드를 생성
var list = document.createElement('ul');
var list_item = document.createElement('li');
var headline = document.createElement('h2');
var list_link = document.createElement('a');
var list_img = document.createElement('img');

// 동적으로 속성노드를 생성 (거의 사용되지 않음)
// 생성된 <a> 요소에 href 속성을 설정(생성해서)
var list_link_href = document.createAttribute('href');
// 생성된 <img> 요소에 src, alt 속성을 설정(생성해서)
var list_img_src = document.createAttribute('src');
var list_img_alt = document.createAttribute('alt');

// 동적으로 생성된 속성노드의 노드 값을 설정
list_link_href.nodeValue = 'https://github.com/yamoo9';
list_img_src.nodeValue = 'https://unsplash.it/300/200/?random';
list_img_alt.nodeValue = 'architecture';
```
## 노드 조작
- `node.appendChild(node)` : 노드 ~ 안에 삽입하기 마지막 자식요소로 넣는다. (부모노드.appendChild(자식요소))
- `node.insertBefore(insert, target)` : 형제요소만들기 (target의 앞에)
- `node.removeChild(delnode)` : 부모노드.removeChild(지울 자식요소)
- `node.replaceChild(alternate, target)` : parentNode.replaceChild(newChild, oldChild) / 특정 부모 노드의 한 자식 노드를  다른 노드로 교체
- `node.cloneNode(boolean)` : 복제
- `node.innerHTML` : HTML구문의 하위 노드들을 가져오거나, 설정
- `setAttribute()` : setAttribute(속성,속성값)
```js
// 요소노드를 요소노드에 붙이려면?
// 부모노드.appendChild(자식노드)
// ul>li>h2>a(href)>img(src, alt)
list.appendChild(list_item);
list_item.appendChild(headline);
list_item.appendChild(list_link);
list_link.appendChild(list_img);

// 속성노드를 요소노드에 붙이려면?
list_link.setAttributeNode(list_link_href);
list_img.setAttributeNode(list_img_alt);
list_img.setAttributeNode(list_img_src);
```

## 노드 생성, 조작 utils 함수
```js
var createElement = function (name) {
    validateError(name, '!string', '요소의 이름을 문자열로 전달해주세요.');
    return document.createElement(name);
};
var createText = function (content) {
    validateError(name, '!string', '요소의 이름을 문자열로 전달해주세요.');
    return document.createTextNode('content');
};
var appendChild = function (parent, child) {
    validateElementNode(parent);
    parent.appendChild(child);
    return child; 
};

// 인자로 생성할 엘리먼트요소의 name과 그 엘리먼트에 담길 content를 넣어 한꺼번에 만들어주는 함수
var createEl = function (name, content) {
    validateError(name, '!string', '첫번째 인자로 요소의 이름을 설정해주세요.')
    var el = createElement(name);
    if (content && isType(content, 'string')){
        var text = createText(content);
        appendChild(el,text);
    }
    return el;
};
```

## 문자열 메서드
    >인자가 무엇인지 알고 싶다면 console.log(arguments); 를 해봐라
- `charAt()`: 숫자값을 넣으면 해당 문자열 반환 (지정한 인덱스에서 문자를 반환)
- `substr(start[, length])`: 특정위치에서 시작하여 length값 만큼의 문자열을 가져온다.
- `substring(indexStart[, indexEnd])`: start에서 마지막 전까지(index)
- `replace(string|regexp, string|function)`: 정규식이나 검색 문자열을 사용하여 문자열에서 텍스트를 바꿈
- `split(string)` : 인자로 들어간 string을 기준으로 조각내서 array로 반환
- `slice(start[, end])`: 첫번째 index에서 끝나는 index 전 까지
- `indexOf(string)`: 인자로 들어간 문자열의 index값
- `trim ()`: 문자열에서 선행 및 후행 공백과 줄 종결자 문자를 제거

## 이벤트
- `onclick`: 클릭시 자바스크립트 구문 실행
- `onfocus`: 입력 필드가 포커스를 취득 할 때 자바 스크립트를 실행
- `onblur`: 사용자가 입력 필드를 떠날 때 자바 스크립트를 실행


## photoShowcase 실습
### 내비게이션 인디케이터를 동적으로 생성한다.
- `<li>`태그에 담긴 data만큼 for문을 돌려서 생성
- 이미지 주소의 맨 뒷자리 숫자값(index)과 alt속성 값을 for문으로 순환시킨다.
- `var data=[{index,alt}]` 로 배열을 만들어 둔다.
```html
<!--동적 생성해야 할 템플릿 코드-->
<li role="presentation">
  <a href class="photo-showcase-indicator" role="tab">
    <img src="https://unsplash.it/100/100?image=" alt="">
  </a>
</li>
```
```js
;(function(global, document, _){
    'use strict';

    var controller = _.selector('.photo-showcase-controller [role=tablist]'); 
    // css선택자 표기법과 비슷 nav.photo-showcase-controller>ul[role=tablist]

    for (var i=0, l=data.length; i<l; i++) {

        var item = data[i];
        var index = item.index; // data배열에 index
        var alt = item.alt; // data배열에 alt

        // 필요한 엘리먼트, 속성 노드들을 만든다.
        var li = _.createEl('li');
        li.setAttribute('role', 'presentation');

        var a = _.createEl('a');
        a.setAttribute('class','photo-showcase-indicator');
        a.setAttribute('href','');

        var img = _.createEl('img');
        img.setAttribute('src','https://unsplash.it/100/100?image=' + index); // data배열에 index값이 들어갈 자리
        img.setAttribute('alt',alt); // data배열에 alt값이 들어갈 자리

        // 각 엘리먼트 요소들을 부모, 자식으로 만든다.
        _.appendChild(li,a); // li>a
        _.appendChild(a,img); // a>img
        _.appendChild(controller,li) // nav>ul>li>a>img
    }
})(window, window.document, window.FDS);
```
### onclick 연결 - a태그에서 자신만의 index값 만들기
- a태그에 이벤트를 연결해줄건데, for문이 문서 실행과 동시해 실행된 후여서 i(index) 값은 11(++index)이 된다. 그래서 어떤 이미지의 a를 클릭해도 i(index)의 값은 11이 나온다. 
- 하지만 각 a는 자기만의 index값을 가져야 한다. for 문이 돌아갈 때 각 a의 고유 index 값을 저장해 두었다가 나중에 onclick을 연결해줄 때 불러온다.
#### 방법1. 클로저 함수 활용 예시
```js
;(function(global, document, _){
    'use strict';

    for ( var i=0, l=data.length; i<l; ++i ) {
        var item = data[i];
        var index = item.index;
        var alt = item.alt;

        // 생략

        a.onclick = function(index) {
        return function(){
            console.log(this, index);
            return false;
        };
        }(i);
    }

})(window, window.document, window.FDS);
```
#### 방법2. 이벤트 바인딩 (속성 <-> 함수)
```js
;(function(global, document, _){
    'use strict';

    for ( var i=0, l=data.length; i<l; ++i ) {
        var item = data[i];
        var index = item.index;
        var alt = item.alt;

        // 생략
        
        a.onclick = changeShowcaseViewWrapper(i);
        // 이벤트 핸들러(함수) 정의
        function changeShowcaseViewWrapper(index) {
            return function changeShowcaseView() {
                // this === 클릭한 <a>
                console.log(this, index);
                // 기본 동작 차단 (구형)
                return false;
            };
        }
    }

})(window, window.document, window.FDS);
```
#### 방법3. 객체의 속성을 추가하여 메모리
- `<a>` 요소노드 === JavaScript 객체
```js
;(function(global, document, _){
    'use strict';

    for ( var i=0, l=data.length; i<l; ++i ) {
        var item = data[i];
        var index = item.index;
        var alt = item.alt;

        // 생략
        
        a.index = i; // 순환문이 돌 때 자신의 index를 기억해 두자.
        a.onclick = changeShowcaseView;
    }
    function changeShowcaseView() {
    // this === 클릭한 <a>
    console.log(this, this.index);
    // 기본 동작 차단 (구형)
    return false;
    };

})(window, window.document, window.FDS);
```
### onclick시 해당 이미지 src주소값 바꿔주기
- src 주소에서 '=' 뒤의 숫자들을 해당 숫자로 바꿔줘야한다.
- 예)`<img src="https://unsplash.it/900/420?image=1068">`
```js
;(function(global, document, _){
    'use strict';

    for ( var i=0, l=data.length; i<l; ++i ) {
        var item = data[i];
        var index = item.index;
        var alt = item.alt;

        // 생략
        
        a.index = i; // 순환문이 돌 때 자신의 index를 기억해 두자.
        a.onclick = changeShowcaseView;
    }
    function changeShowcaseView() {
        var source = data[this.index]; // i
        var showcase = _.selector('.photo-showcase img');
        showcase.setAttribute('alt', source.alt); 
        var showcase_old_src = showcase.getAttribute('src');

        // 방법 1.
        // .slice(), .indexOf() 를 활용한 예시
        var end_index = showcase_old_src.indexOf('=') + 1; // 공통으로 들어가는 =의 뒷자리 index => 아래 slice()의 두번째 인자는 끝나는 인덱스의 전까지 반환하기 때문에 
        var showcase_new_src = showcase_old_src.slice(0, end_index) + source.index; // 'https://unsplash.it/900/420?image=' + 

        // 방법 2.
        // RegExp, replace() 를 활용한 예시
        var showcase_new_src = showcase_old_src.replace(/=.+/, function(){ // '='뒤로 문자열(.)모두(+) 바꿔라
        return '=' + source.index;
        });

        showcase.setAttribute('src', showcase_new_src);
        // 기본 동작 차단 (구형)
        return false;
    };

})(window, window.document, window.FDS);
```
### 접근성 개선
- 브라우저에서 showcase 영역에 마우스 hover를 해야지만 이미지 리스트들이 보여지고(opacity: 0; -> opacity: 1;) 키보드 focus로는 이미지 리스트에 접근할 수 없다.
- hover 효과를 준 엘리먼트는 div.photo-showcase-container 인데 div태그에는 키보드 focus를 줄 수 없다.
- 그렇다고 div를 a로 바꿔줄수도 없다. 왜냐햐면 a태그 안에는 a태그나 input태그 등은 자식요소가 될 수 없다.
- 뭐가 필요하냐?
- 포커스가 됐습니다 상태 클래스가 필요하다.
- 첫번째 요소(li)에 `onfocus` 이벤트 - focus가 되면 div에 'active'클래스가 생성된다.
- 마지막 요소(li)에 `onblur` 이벤트 - focus가 끝나면서 div에 'active'클래스가 사라진다.
```js
;(function(global, document, _){
    'use strict';

    // 문서객체 참조
    var container        = _.selector('.photo-showcase-container');
    var container_active = 'active';
    var indicator_first  = _.selector('li:first-child a', controller);
    var indicator_last   = _.selector('li:last-child a', controller);

    // focus, blur 이벤트 감지
    indicator_first.onfocus = function() {
        // container 요소에 활성화 클래스를 추가한다.
        var container_class = container.getAttribute('class');
        container_class += ' ' + container_active; // <div class="photo-showcase-container active"> 클래스 여러개 줄때는 공백문자 필요
        container.setAttribute('class', container_class);
    };

    indicator_last.onblur = function() {
        // container 요소에 활성화 클래스를 제거한다.
        var container_class = container.getAttribute('class');
        container_class = container_class.replace(container_active, '').trim(); // active를 빈문자로 바꾼뒤 공백문자는 잘라낸다(trim)
        container.setAttribute('class', container_class);
    };

})(window, window.document, window.FDS);
```
- js로 만들어 놓은 active 클래스에 스타일을 준다.
- div태그에 active클래스가 생기면 opcity:1; 을 주어 화면에 보여지게 한다.
```css
.photo-showcase-container:hover .photo-showcase-controller,
.photo-showcase-container.active .photo-showcase-controller {
  opacity: 1;
}
```