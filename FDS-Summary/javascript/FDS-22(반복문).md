FDS-22-반복문
========

### << if 문에서 거짓으로 판단하는 것 >>
- `false`
- `undefined`
- `null`
- `0`
- `NaN`
- the empty string `("")`

### << for문의 기본 >>
- i=100 하니까 100만큼 나오고 i=5하니까 5만큼 나온다
```js
for ([초기문]; [조건문]; [증감문])
  문장

for ( var i=100; i; --i{
    console.log();
}
```

### <<랜덤 함수 만들기>>
- `Math.random()` : 0 ~ 1 실수

### << 흐름제어와 오류처리 >>
- `indexOf()` : 배열에서 지정된 요소를 찾을 수있는 첫 번째 인덱스를 반환하고 존재하지 않으면 -1을 반환한다./개체 안에서 부분 문자열이 처음 나오는 문자 위치를 반환
```js
var array = [2, 9, 9];
array.indexOf(2);     // 0
array.indexOf(7);     // -1
array.indexOf(9, 2);  // 2
array.indexOf(2, -1); // -1
array.indexOf(2, -3); // 0
```

- `slice()` : slice([begin[, end]]) / 추출을 시작하는 인덱스(0부터 셈). / 추출을 끝내는 인덱스(0부터 셈). slice는 end(를 포함하지 않음)까지만 추출 / 음수 인덱스일 때, end는 열 끝으로부터 오프셋을 나타냄 /  slice(2,-1)은 열의 3번째부터 끝에서 2번째 요소까지 추출

- `new Date()` : 현재 날짜와 시간이 기본으로 세팅됨
  - `new Date(dateString)` : 사용자가 지정한 날짜 문자열을 기본으로 세팅됨
  - `new Date(year, month, day, hours, minutes, seconds, milliseconds)` : 각 요소들을 직접 지정하여 세팅함
  - `getFullYear()` : 년도 얻기 / 왜 FullYear 나면 1999년에서 2000년도로 넘어가면서 날짜나 시각을 다루는 과정에서 오류가 일어나는 문제 때문에 생겨남
  - `getTime()` : 1970년 1월 1일 이후 부터 지금까지의 시간을 밀리세컨드 단위의 숫자로 얻기
  - `setFullYear()` : 년도를 세팅하기
  - `getDay()` : 요일 값 숫자로 얻기


### << 고전예제 : 요일 출력 >>
```js
console.groupCollapsed('고전 예제: 요일 출력');

var weekdays = ["일", "월", "화", "수", "목", "금", "토"];
var today    = new Date();
var weekday  = today.getDay();
var printDay = function(day) {
  validateError(day, '!string','전달인자 유형은 문자열이어야 합니다.');
  return '오늘은 ' + day + '요일입니다';
};

console.log('// if문');
if ( weekday === 0 ) { console.log(printDay(weekdays[0])); }
else if ( weekday === 1 ) { console.log(printDay(weekdays[1])); }
else if ( weekday === 2 ) { console.log(printDay(weekdays[2])); }
else if ( weekday === 3 ) { console.log(printDay(weekdays[3])); }
else if ( weekday === 4 ) { console.log(printDay(weekdays[4])); }
else if ( weekday === 5 ) { console.log(printDay(weekdays[5])); }
else if ( weekday === 6 ) { console.log(printDay(weekdays[6])); }
else { console.warn('존재하지 않는 요일입니다'); }

console.log('// switch문');
switch(weekday) {
  case 0: console.log(printDay(weekdays[0])); break;
  case 1: console.log(printDay(weekdays[1])); break;
  case 2: console.log(printDay(weekdays[2])); break;
  case 3: console.log(printDay(weekdays[3])); break;
  case 4: console.log(printDay(weekdays[4])); break;
  case 5: console.log(printDay(weekdays[5])); break;
  case 6: console.log(printDay(weekdays[6])); break;
  default: console.warn('존재하지 않는 요일입니다');
}

console.groupEnd('고전 예제: 요일 출력');
```

- `Console.warn()` : 경고 메시지를 출력한다. 문자열 치환(string substitution)과 추가 인자를 사용할 수 있다.
- `console.log('--------------------');` : console창에 가로줄 긋기