FDS-22-반복문
========

## << if 문에서 거짓으로 판단하는 것 >>
- `false`
- `undefined`
- `null`
- `0`
- `NaN`
- the empty string `("")`

## << for문의 기본 >>
- i=100 하니까 100만큼 나오고 i=5하니까 5만큼 나온다
```js
for ([초기문]; [조건문]; [증감문])
  문장

for ( var i=100; i; --i{
    console.log();
}
```

## <<랜덤 함수 만들기>>
- `Math.random()` : 0 ~ 1 실수
- `Math.floor()` : 반내림
- `Math.round()` : 반올림

## << 흐름제어와 오류처리 >>
```js
// 상태
var is_opened = true;

// {} 블록문 내에 var 변수 선언이 있을 경우 주의! (호이스트 현상)
if ( !true ) {
  var is_closed = false;
}
console.log(is_closed); // undefined 
// is_closed 는 호이스팅 때문에 위에서 호출됨. if 블록문 안에서 false값을 가졌지만, if문이 false(!true)이기 때문에 실행 되지 않았으므로 is_closed의 값은 그대로 undefined

if ( is_opened ) {
  // 열려져 있는 상태 -> 닫힌 상태
  // 상태 변경
  var is_opened = false;
  // var is_opened = !is_opened;
} else {
  // 닫힌 상태 -> 열린 상태
  is_opened = true;
  // is_opened = !is_opened;
}

// if ... else 구문을 한 줄로 줄여 사용한 형태
is_opened = !is_opened; // open <- toggle -> close
```


## << 고전예제 : 요일 출력 >>
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

## << switch 기본 문법 >>
```js
switch (식) {
    case 값:
        문;
        brea
    default:
        break;
}
```

## << 3항 연산 조건문 >>
- 식
```js
isType(weekday, 'string') ? 'weekday is String' : 'weekday isn\'t String';
```

## << try / catch / throw / finnally
- 한 블록에서 throw된 오류가 다른 블록에서 처리되는 코드 블록을 설정 try 블록 내부에서 throw되는 오류는 catch 블록에서 catch된다.
- try블록에서 오류가 발생하면 프로그램 제어가 catch에 전달된다.(exception)값은 try블록에서 발생된 오류값. 오류가 발생하지 않으면 catch 블록의 코드는 실행되지 않음 / try 블록의 모든 문이 실행되고 catch블록에서 오류처리가 수행되고 나면 오류처리의 여부와 상관없이 finally블록의 코드가 실행된다.
- throw 문을 사용하여 오류를 다시 throw하면 오류를 다음 수준까지 전달할 수 있음
```js
try {
    tryStatements
}
catch(exception){
    catchStatements
}
finally {
    finallyStatements
}
```

```js
try {
    console.log('try statement');
    // 명령이 실행되었을 때
    // 오류가 발생하지 않았거나
    var last_weekday = weekday.pop();//오타 발생! s가 빠져있다.
    // 오류가 발생했거나
    console.log('last_week:',last_weekday)
}catch(error){
    // throw VS console.log(error.message); //오류 잡아서 오류 메시지 출력
    // console.error()와 달리 throw는 뒤 구문을 중단한다.
    // console.error(error.message); //오류 잡아서 오류 메세지 출력
    throw error.message;
    last_weekday = weekdays.pop();
    console.log(last_weekday);
}
```

## << for in 문 >>
- 개체의 각 속성이나 배열의 각 요소에 대해 하나 이상의 문을 실행
- '속성' in 객체
- 객체의 속성을 순환하여 처리
- 객체는 배열과 달리 length 속성이 존재하지 않는다.
- 하여 객체를 순환하려면 for...in 문을 사용한다.
- 배열 또한 for...in문을 사용할 수 있으나, 속도가 느려 for문을 사용하는 것이 좋다.
```js
for (variable in [object | array]) {
    statements 
}

for ( var prop in han ) {
  // 객체 자신이 소유한 속성인지를 판단하여
  // 자신의 속성일 경우만 출력하라.
  if ( han.hasOwnProperty(prop) ) {
    // han 객체의 속성 prop을 순환하여 처리한다.
    console.log('han 객체의 속성:', prop);
    // han.age === han['age']
    // 순환 과정에서 속성 이름을 알 수 없기에,
    // 변수를 사용한 객체 속성 접근법을 사용해야 한다.
    // han[prop]
    console.log('han 객체의 값:', han[prop]);
  }
}
```


## << 상속 >>
- `create()` : 지정된 프로토타입 객체 및 속성(property)을 갖는 새 객체를 만든다.
```js
// 객체(부모)
var parent = {
  name: '김훈남',
  age: 67,
  job: '농부',
  drive: function(mobil) {
    mobil = mobil || '경운기';
    return this.job + '인 ' + this.name + '씨가 ' + mobil + '을(를) 타고 드라이브 합니다.';
  }
};
// 객체(자식) <- 부모객체의 능력을 상속(Inheritance)
var child = Object.create(parent);
// 자식 객체에 속성을 추가 (부모 객체에는 없는 속성)
```

- `hasOwnProperty()` : 객체가 특정 프로퍼티를 가지고 있는지를 나타내는 불리언 값을 반환
- 모든 객체는 hasOwnProperty 를 상속하는 Object의 자식이다. 이 메소드는 객체가 특정 프로퍼티를 자기만의 직접적인 프로퍼티로서 소유하고 있는지를 판단하는데 사용된다.  in 연산과는 다르게, 이 메소드는 객체의 프로토타입 체인을 확인하지는 않는다.
```js
for ( var prop in han ) {
  // 객체 자신이 소유한 속성인지를 판단하여
  // 자신의 속성일 경우만 출력하라.
  if ( han.hasOwnProperty(prop) ) {
    // han 객체의 속성 prop을 순환하여 처리한다.
    console.log('han 객체의 속성:', prop);
    // han.age === han['age']
    // 순환 과정에서 속성 이름을 알 수 없기에,
    // 변수를 사용한 객체 속성 접근법을 사용해야 한다.
    // han[prop]
    console.log('han 객체의 값:', han[prop]);//.prop로 접근할 수 없기에 []를사용하였다.
  }
}
```
- `Console.warn()` : 경고 메시지를 출력한다. 문자열 치환(string substitution)과 추가 인자를 사용할 수 있다.
- `console.log('--------------------');` : console창에 가로줄 긋기
- `slice()` : slice([begin[, end]]) / 추출을 시작하는 인덱스(0부터 셈). / 추출을 끝내는 인덱스(0부터 셈). slice는 end(를 포함하지 않음)까지만 추출 / 음수 인덱스일 때, end는 열 끝으로부터 오프셋을 나타냄 /  slice(2,-1)은 열의 3번째부터 끝에서 2번째 요소까지 추출

- `new Date()` : 현재 날짜와 시간이 기본으로 세팅됨
  - `new Date(dateString)` : 사용자가 지정한 날짜 문자열을 기본으로 세팅됨
  - `new Date(year, month, day, hours, minutes, seconds, milliseconds)` : 각 요소들을 직접 지정하여 세팅함
  - `getFullYear()` : 년도 얻기 / 왜 FullYear 나면 1999년에서 2000년도로 넘어가면서 날짜나 시각을 다루는 과정에서 오류가 일어나는 문제 때문에 생겨남
  - `getTime()` : 1970년 1월 1일 이후 부터 지금까지의 시간을 밀리세컨드 단위의 숫자로 얻기
  - `setFullYear()` : 년도를 세팅하기
  - `getDay()` : 요일 값 숫자로 얻기
- `indexOf()` : 배열에서 지정된 요소를 찾을 수있는 첫 번째 인덱스를 반환하고 존재하지 않으면 -1을 반환한다./개체 안에서 부분 문자열이 처음 나오는 문자 위치를 반환
```js
var array = [2, 9, 9];
array.indexOf(2);     // 0
array.indexOf(7);     // -1
array.indexOf(9, 2);  // 2
array.indexOf(2, -1); // -1
array.indexOf(2, -3); // 0
```