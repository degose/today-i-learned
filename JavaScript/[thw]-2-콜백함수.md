tryhelloworld [자바스크립트와 웹프론트엔드] 2 - callback function
========


## << Callback Function >>
- 조건을 등록해 두고 그 조건을 만족한 경우, 나중에 호출되는 함수
- `setTime(실행할 메서드(함수), 지연할 시간)`
    - millisecond(1/1000초)eksdnl
    - timerld를 반환함
```js
function callback(){
    console.log('callback function is called');
}
setTimeout(callback, 3000);
// 3초뒤에 콜백함수가 출력
setInterval(callback, 5000);
// 5초를 두고 계속 실행 된다. (개발자 도구 왼쪽에 숫자값이 계속 오른다.)
clearInterval(2);
// 2번 콜백 함수가 멈춘다.
```