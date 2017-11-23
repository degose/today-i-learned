## 이벤트 위임(event delegation)

* 해당 엘리먼트보다 상위 엘리멘트에 이벤트핸들러를 달아 놓고 버블링 현상을 이용해 상위 엘리먼트에서 Event가 발생한 node를 확인는 로직을 넣어 이벤트를 실행하게 해주는 원리
* 등록되는 Event Handler의 수를 줄일 수 있다.(성능에 도움)
* 응용 한 예
    * 해커톤 groupTodolist 프로젝트에서 삭제버튼을 if (ev.target.localName === ‘button’ && target.classList.contains(‘delete’)) { code} 식으로 확인하는 코드를 넣어서 활용함
* event propagation(이벤트 전파)
    * event Bubbling : 자식 - - -> 부모
    * event Capturing : 부모 - - -> 자식(이벤트 발생)
    * 캡처링부터 시작하여 버블링으로 종료
    * 캡처링은 IE8 - 지원하지 않는다.
    * addEventListener(dddd,dddd, true) true=> 캡처링, false or 미설정 => 버블링