FDS-42-실습(accordionUI,components)
========

## 실습 (accordion UI 라디오 버튼으로 바꾸기)

### pug
- sass처럼 partials를 지원해주지 않는다.

### void
- 주어진 식(expression)을 실행하고, undefined 반환
```js
var $component = void 0,
    $lists = void 0,
    $labels = void 0,
```

### eq , trigger
- `eq`
  - `.eq( index )`
  - 일치하는 요소를 지정된 index에있는 요소로 줄여서 반환
  - jQuery 반환
- `trigger`
  - `.trigger( eventType [, extraParameters ] )`
  - jQuery 반환
  - 특정 이벤트 유형에 대해 선택된 요소에 연결된 모든 핸들러와 동작(behavior)을 실행
  - 이벤트가 발생할 때 실행될 함수나 .bind() 함수로 연결된 어떤 이벤트 핸들러를 강제로 실행준다. .trigger() 함수를 사용해서 사용자가 일으킬 이벤트를 임의적으로 순서에 따라 발생시킬 수 있다.
  - 시뮬레이션
```js
$labels.eq(1).trigger('click');
```

### random 함수 만들기
```js
;(function($){
  'use strict';

  if(!$.random) {
    // Static Method
    // Utility Method
    // Class Method
    jQuery.random = n => {
      return Math.floor(Math.random() * n);
    };
  }
  
})(window.jQuery);

;(function (global, $) {
  'use strict';

  /** 모듈 내 지역 변수 */

  /** 초기화 함수 */
  function init() {
    // 객체 참조
    $component = $('.ui-accordion');
    $lists = $component.find('.menu-list'); // .find() 인스턴스 메서드 사용
    $labels = $('.menu-label a', $component); // context 전달인자 사용
    // 이벤트 바인딩
    bind();
    // 초기 실행
    $lists.hide(); // 모든 리스트 감추기
    var n = $.random($labels.length);
    $labels.eq(n).trigger('click'); // 특정 레이블 활성화 클릭 실행 // eq equel // trigger -> 방아쇠 이벤트를 발생시킨다.
  }
  /** 이벤트 핸들링 */
 
  /** 이벤트 핸들러 */

  // 초기화 실행
  init();
})(window, window.jQuery);
```

### is()
- `.is( selector )` 인자로 seletor, function, elements, jQuery seletion 등이 올 수 있다.
- selector, element 또는 jQuery 객체에 대해 현재 일치하는 요소 집합을 검사하고 이러한 요소 중 하나 이상이 주어진 인수와 일치하는 경우 boolean 반환
```js
$( "li" ).click(function() {
  var li = $( this ),
    isWithTwo = li.is(function() {
      return $( "strong", this ).length === 2;
    });
  if ( isWithTwo ) {
    li.css( "background-color", "green" );
  } else {
    li.css( "background-color", "red" );
  }
});
```

### toggle()
- `.toggle( [duration ] [, complete ] )`
- jQuery 반환
- duration: number
- complete: function (애니메이션 함수 같은 것도 올 수 있음)


### toggleMultiList 함수, toggleList 함수
```js
function toggleMultiList(e) {
  e.preventDefault(); // 기본 동작 차단
  let $this = $(e.target); // 클릭한 대상 jQuery화 참조
  let $list = $this.parent().next();
  // Toggle List % Label
  toggleList($this, $list);

  // if ( $list.css('display') === 'none' ) {
  // if (!$list.is(':visible')) {
  //   $list.show(time);
  //   $this.addClass('is-active');
  // } else {
  //   $list.hide(time);
  //   $this.removeClass('is-active');
  // }
}
function toggleList(label, list) {
  label.toggleClass('is-active');
  list.toggle(time);
}
```
### toggleSingList 함수 
- 제어 방법 1: 하나 하나 제어( 위에 toggleList 함수와 별개로 )
```js
function toggleSingleList(e) {
  e.preventDefault(); // 기본 동작 차단
  let $this = $(e.target); // 클릭한 대상 jQuery화 참조
  let $list = $this.parent().next();
  let $actived = $labels.filter('.is-active')
  // 현재 열린 리스트와 is-active를 가진 <a> 요소를 제어

  // 그런데 이미 활성화된 요소를 또 누르면 다시 열렸다 닫혔다 하는 이슈가 발생;;
  // 활성화된 레이블과 사용자가 클릭한 레이블이 일치한다면
  // 함수를 종료하라.
  if ( $actived.is($this)) {return;}

  // is-active 클래스를 가진 <a> 요소에게서 해당 클래스를 제거한다.
  // $labels는 집합. 어떤 메서드를 쓰는 게 좋을까?
  $actived.removeClass('is-active');
  // $lists 중 열린 리스트(:visible)를 찾아 닫아준다. hide(time)
  $lists.filter(':visible').hide(time);
  // $this 객체에 is-active 클래스를 추가한다.
  $this.addClass('is-active');
  // $list 객체를 펼처준다. show(time)
  $this.show(time);
}
```
- 제어 방법 2: toggleList 함수를 만들어 재사용
```js
function toggleSingleList(e) {
  e.preventDefault(); // 기본 동작 차단
  let $this = $(e.target); // 클릭한 대상 jQuery화 참조
  let $list = $this.parent().next();
  let $actived = $labels.filter('.is-active')
  // 현재 열린 리스트와 is-active를 가진 <a> 요소를 제어

  // 그런데 이미 활성화된 요소를 또 누르면 다시 열렸다 닫혔다 하는 이슈가 발생;;
  // 활성화된 레이블과 사용자가 클릭한 레이블이 일치한다면
  // 함수를 종료하라.
  if ( $actived.is($this)) {return;}

  // toggleList()를 실행하여 현재 열린 리스트와 활성화된 레이블을 비활성화 한다.
  toggleList($actived, $lists.filter(':visible'));
  // toggleList()를 실행하여 클릭한 레이블과 연결된 리스트를 펼쳐준다.
  toggleList($this, $list);
}
```
- sass도 바꿔준다. active되면 더이상 cursor도 손가락 모양이 아닌 기본값으로 하게 해서 -> 클릭할 수 없음을 보여준다.
```css
.menu-label a
  transition: all 0.4s ease
  &.is-active
    background: #00d1b2
    color: #fff
    cursor: default
```

### cache 함수
- 성능향상에 도움
- 매번 jQuery 인스턴스 메서드를 불러오지 않고 한번 불러오면 캐시 데이터에 저장해서 불러오면 되니까.

### filter()
- `.filter( selector )` 인자로 selector, elements, function, jQuery 객체 넣을 수 있다.
- jQuery 반환


### even 홀수,짝수 개념 css와 제이쿼리 다른 이유
- index가 0부터 시작하기 때문에


## Sizzle 엔진
- 참고: <http://blog.naver.com/PostView.nhn?blogId=jjoommnn&logNo=130145313318>
- 멀티브라우저 오픈 소스 셀렉터 엔진
- jQuery에서 selector 엔진으로 sizzle엔진을 사용한다.
