FDS-21-연산자/데이터검증/utils파일
========

# << 액티비티 테스트 >>
#### <<참조가 되는 데이터 유형>>
- Object `var glass = {};`
- Array `var glasses = [];`
- Function `var watchGlass = function(){};`
#### <<Constructor로 판별할 수 있는 type>>
- `.constructor` : 속성은 객체가 소유한 것이기에, 객체가 아닌 것을 검증할 수 없다. (오류발생) 객체가 아닌 것 : null, undefined
- Object , Array, Number, String, Boolean, Function (생성자들)
#### <<배열>>
```js
var arr = [2,7,5,8];

arr.length => 4
arr[3] => 8
typeof arr => Array //오답 => `typeof`는 Array를 Object로 나타낸다. 
arr.push(9) => arr = [2,7,5,8,9]; //마지막 요소 추가 `pop`은 마지막 요소 삭제
arr.unshift(4) => arr = [4,2,5,8]; //shift: 배열에서 첫 번째 요소를 제거하여 반환 / unshift: 배열 시작에서 새 요소를 삽입
```

Array의 method
```js
var arr = ['float: left', 'color:#333', 'margin: 0'].join(';'); => ['float: left;color: #333; margin: 0']
 
var arr = [2, 5, 7, 4].push(7); => [2, 7, 5, 7, 4]
var arr = [4, 9, 1, 2].pop(); => [4, 9, 1, 2]
var arr = ['apple', 'banana', 'grape'].splice(2, 1); => ['grape']
var arr = ['apple', 'banana', 'grape'].shift() => ['banana']
```
#### <<연산자>>
- (a=1, b=2)
```js
var c = a++; // 1 (다음 라인에서 +1이 된다.)
var c = ++a; // 2 (이미 더해진 값이 출)
var c = b; // 2
var c = b--; // 2 (다음 라인에서 -1이 된다.)
var c = --a+b; // 0 + 2 = 2
```
```js
1 =='1' //true
typeof null == typeof Array() // 오답 =>typeof는 Array를 Object로 반환한다.
null == undefined 
null === undefined //false
1 === '1' //false 
```
```js
var a = '1' + '2'; //'12'
var a = (3+'') * (4+'');
var a = (2*6)+''; //12 + '' = '12'
var a = (12).toString()//'12'
```

#### <<Javascript 내장함수>>

#### <<객체 내부 속성에 접근방법>>
```js
object.property
object['property']
```


##<< 디버거 >>
- `debugger`: 브레이크 포인트 (의심이 되는 부분에 디버거를 줘서 확인을 해봐야한다.)

## << ++, -- 연산자 >>
```js
var n = 100;

// n + 30
n = n + 30;
n = + 30;
n += 30;

var k = 9;

// k + 1 => '식' 값을 반환한다.
k = k + 1; // 값 복사 10으로 교체
k += 1; // 11
K++; // 11 "후 증가" (아직은 11 다음라인에서 12)
++k; // 13 "선 증가"

--k; // 선 감소
k--; //후 감소

var k = 11;
k % 3 // 2
++k % 3 //0
k %= 4;
// %=; 나머지 연산자 => 캐러셀처럼 순환하는 구조에 쓰일 수 있다.
0 == false // true
1 == '1' //true

0 === false // false
null == false //false
undefined == false //false
// 그러므로 ===를 붙이는게 좋다.
```

## << 데이터 유형 검증 >>
1. typeof
2. instanceof
3. .constructor
4. type()

- 데이터 검증 시뮬레이션을 위한 데이터 객체
- 리터럴 / date만 생성자 표현식
```js
var types = {
    'num': 19,
    'str': "h1, there",
    'boo': false,
    'fnc': function(){},
    'arr': [], //Object
    'obj': {},
    'nothing': [null,undefined], //undifined
    'date': new Date() //Object
};
```
### 1. typeof, typeof는 함수가 아니다. ()는 함수 실행 연산자가 아니라, 식을 묶기 위한 괄호
typeof는 배열을 배열이라 하지 않고 Array라고 한다.
typeof는 null을 Object라고 한다.
typeof 를 쓰지마셈.
```js
var tester = classUsingArray[0];
// console.log(tester);

console.log('typeof tester.name:',typeof tester.name);
console.log('typeof tester.age:',typeof tester.age);
console.log('typeof tester.family:',typeof tester.family); // family는 Array(배열)인데 Object로 나온다.
console.log('typeof tester.school:',typeof tester.school); // school은 null인데 Object로 나온다.
// console.log('typeof tester.grade:',typeof tester.grade); // school이 null이기 때문에 school.grade의 값을 불러오면 오류가 뜬다.
```
2. typeof 문제점
- null, Array, 그 외 Host Object 모두 'Object'라고 말하는 문제

3. Array 를 올바르게 판별하는 방법
- ES5(2009) -> Array.isArray(data) // true, false 
- is 라고 물어보면 불리언 값을 반환한다.
```js
Array.isArray(tester.family); // true
```
// 폴리필? 브라우저 호환 가능한 것을 만들어 쓰면 된다.
// 바벨??

### 2. instanceof
- 클래스(Class)란?    <--->   생성자(Constructor)   <---> 추상적인 설계 도면
- 생성자 이름은 Constructor처럼 앞글자는 대문자로 이름을 지어주면 좋다. 디자인패턴 / new를 붙여주는게 좋다.(스테이틱 모드)
- 인스턴스(Instance)란?    <--->   객체(Object)    <--->  실체화된 사물(제품)

- 객체 instance of 생성자 // 객체 너는 생성자로부터 만들어진 거니? // true or false // 객체가 아닌 null, undifined를 넣으면 안된다.
```js
tester.family instanceof Array // true
tester.family instanceof String // false
tester.family instanceof Number // false
tester.family instanceof Object // true //왜냐면 배열은 객체로부터 나왔기때문에 

types.date instanceof Date // true 

```
- 원시 데이터 유형
- instanceof 객체를 통해 생성자가 맞는지 검증하는 수단 -> 원시 데이터 유형은 instanceof로 검증할 수 없다.
- 숫자 값, 문자 값, 논리 값, null, undefined
```js
90 instanceof Number;  //false

console.log('90 instanceof Number:',90 instanceof Number); //false
console.log('new Number(90) instanceof Number:',new Number(90) instanceof Number); //true
console.log('Number("90") instanceof Number:',Number("90") instanceof Number); //false
```

### 3. .constructor
```js
console.group('constructor 속성은 모든 객체가 태어날때부터 꼬리표처럼 가지고 태어난다');

// 객체인 유형
console.log('types.num.constructor:',types.num.constructor === Number);
console.log('types.str.constructor:',types.str.constructor === String);
console.log('types.boo.constructor:',types.boo.constructor === Boolean);
console.log('types.fnc.constructor:',types.fnc.constructor === Function);
console.log('types.arr.constructor:',types.arr.constructor === Array);
console.log('types.obj.constructor:',types.obj.constructor === Object);
console.log('types.date.constructor:',types.date.constructor === Date);

// 객체가 아닌 유형 null, undefined
// .constructor 속성은 객체가 소유한 것이기에, 객체가 아닌 것은 검증할 수 없을 뿐더러 오류를 발생시킨다.
console.log('types.nothing[0].constuctor:',types.nothing[0].constuctor); //null
console.log('types.nothing[1].constuctor:',types.nothing[1].constuctor); //undefined

console.groupEnd('constructor 속성은 모든 객체가 태어날때부터 꼬리표처럼 가지고 태어난다');
```

### 4. type() 유틸리티 함수

- `.call`

// 함수가 처리하는 로직(Logic) 설계
// 원리 이해, 재사용 가능하게 설정

// 올바른 데이터 유형 검증 (심지어 객체가 아닌 것 포함)
// null, undefined 도 검증 가능

// 생성자(일급함수객체)
// 생성자.prototype ----> 프로토타입 객체 {}
// 객체생성 = new 생성자(일급함수객체)
// 생성자로부터 생성된 객체의 모든 능력은 어디서 올까? (힘의 근원)
// 프로토타입 객체 ?? - >

// Object.prototype.constructor 
// readonly 아니고 생성자를 임의로 바꿀 수 있다. 

// Javascript 메서드 빌려쓰기 패턴
// 새.날다()
// 사람.걷다()
// Function.prototype.call  //모든 함수가 가지고 있는 call
// 새.날다.call(사람)
```js
function Bird() {}

Bird.prototype.fly = function() {};

var myBird = new Bird();

myBird.fly();

function Human() {}

Human.prototype.walk = function() {};

var me = new Human();

me.walk(); // ok

me.fly(); // has not

Bird.prototype.fly.call(me); // me.fly();

Object.prototype.toString.call(new Date); //'[object Date]'
Object.prototype.toString.call(new Date()).silce(8) // "Date]"
Object.prototype.toString.call(DATA).silce(8,-1).toLowerCase(); // "Date"
```

## utils 파일 함수 만들기
[Tip! .js 파일에서 (control + option + d ) * 2 doc 실행]

### << JavaScript 데이터 유형을 완벽하게 문자열로 반환하는 유틸리티 함수 >>
- typeof(), .construct,.. 등등 데이터 유형을 완벽하게 반환해주지 않으니까 함수로 만들어 쓴다.
- `type()`이라는 함수를 만들건데, 인자로 모든 유형의 `data`를 받고 return값으로는 소문자 `string`을 반환할거야.
- `.call`을 이용해서. 생성자의 객체`prototype`의 속성을 참조해 올거야.
- `toString`: 데이터를 문자열로 형 변형 함수 / `slice()` : 배열의 일정 부분을 반환 메서드 / `toLowerCase()`: 소문자로 변형 메서드
- `Object`생성자의 객체 `prototype`의 속성 `toString`을 `call`로 참조한 값[object Data]을 `slice`로 앞 0번째서 부터 8번째자리부터 반환시킬거고, 마지막 ]을 -1로 삭제한 뒤에, `toLowerCase`로 소문자로 반환시킬거야.

```js
/**
 * JavaScript 데이터 유형을 완벽하게 문자열로 반환하는 유틸리티 함수
 *
 * @param {any} data - JavaScript 모든 데이터 유형
 * @returns {string} - 소문자로 데이터 유형 이름을 문자열로 반환
 */
function type(data) {
  return Object.prototype.toString.call(data).slice(8,-1).toLowerCase();
}
```

### << JavaScript kind(두번째 인자)의 형이 'string'이 아닌 경우 에러메세지를 반환하는 함수 >>
- 보통 is가 앞에 들어오는 함수는 불리언 값을 반환한다.
- 데이터 검증(유효성 검사: validate)
- `isType()`이라는 함수를 만들건데, 인자1로 모든 유형의 `data`를 받고 인자2로 소문자 유형의 string `kind`를 받을 거야
- return값으로는 `boolean`을 반환할거야.
- 만약에 인자2 `kind`가 함수`type()`넣어져서 반환된 값이 `'string'`이 아니면(`!==`) `throw` 문자열 값이 보여진다. return이 되려면, `type(data)`의 값이 `kind`('string')이어야 한다.
```js
/**
 * 
 * 
 * @param {any} data - JavaScript 모든 데이터 유형
 * @param {string} kind - 데이터 유형 이름(소문자)
 * @returns {boolean} - 데이터 일치 검증 결과를 참/거짓으로 반환
 */
function isType(data, kind){
    if (type(kind) !== 'string'){
        throw 'kind 전달 인자는 문자열이 전달되어야 합니다.';
    }
    return type(data) === kind;
}
```



### << JavaScript 데이터 유형을 검증하여 참 / 거짓으로 반환하는 유틸리티 함수 >>
- 목적??
- 위 방법과 다른 방법
- `validate` ???? 함수임??
- `validate`의 인자1`kind`의 값이 문자열이 아닌경우 `'!string'` 
```js
/**
 * JavaScript 데이터 유형을 검증하여 참/거짓을 반환하는 유틸리티 함수
 *
 * @param {any}     data - JavaScript 모든 데이터 유형
 * @param {string}  kind - 데이터 유형 이름(소문자)
 * @returns {boolean}    - 데이터 일치 검증 결과를 참/거짓으로 반환
 */
function isType(data, kind) {
  validate(kind, '!string', '2번째 전달인자는 문자열이어야 합니다');
  return type(data) === kind;
}
```


### << 전달된 데이터, 데이터 유형을 검증하여 값이 일치할 경우, 오류를 발생시키는 유틸리티 함수 >>
- 목적??
- `valid`라는 함수를 만들건데 만약 인자1`data`가 `type(data)`에 대입된 값이 인자2 `kind`와 `===`일치하면(참) return 값을 반환, 거짓일 경우 예외(throw)로 `error_message`를 반환하는데 `||` 이게 
```js
/**
 * 전달된 데이터, 데이터 유형을 검증하여 값이 일치할 경우, 오류를 발생시키는 유틸리티 함수
 *
 * @param {any} data             - JavaScript 모든 데이터
 * @param {string} kind          - 오류 검증을 위한 문자열 데이터
 * @param {string} error_message - 오류 메시지
 * @returns {string}             - 유효한 경우 출력되는 메시지
 */
function valid(data, kind, error_message) {
  if ( type(data) === kind ) {
    throw error_message || '두 값은 동일하기에 오류입니다.';
  }
  return '오류는 발생하지 않았습니다';
}
```


### << 
- 목적???
- 

```js
/**
 * 전달된 데이터, 데이터 유형을 검증하여 값이 불일치할 경우, 오류를 발생시키는 유틸리티 함수
 *
 * @param {any} data             - JavaScript 모든 데이터
 * @param {string} kind          - 오류 검증을 위한 문자열 데이터
 * @param {string} error_message - 오류 메시지
 * @returns {string}             - 유효한 경우 출력되는 메시지
 */
function invalid(data, kind, error_message) {
  if ( type(data) !== kind ) {
    throw error_message || '두 값이 다르기에 오류입니다.';
  }
  return '오류는 발생하지 않았습니다';
}
```



### << 
- 목적??? 오류 메세지속 '!
- `.indexOf(i)`: 배열에서 i가 있는 순서??? ''번째 값을 반환하는 메서드
- `validate`라는 함수를 만들건데, 만약 인자2 `kind`의 배열에서 !가(`indexOf(!)`) 있는 번째수가 -1 보다 클경우 함수 `invalid`에 대입해보고, -1보다 같거나 작을경우, 함수 `valid`에 대입해라.
```js
/**
 * 전달된 데이터, 데이터 유형을 검증하여 조건이 참일 경우, 오류를 발생시키는 유틸리티 함수
 *
 * @param {any} data             - JavaScript 모든 데이터
 * @param {string} kind          - 오류 검증을 위한 문자열 데이터
 * @param {string} error_message - 오류 메시지
 */
function validate(data, kind, error_message) {
  if ( kind.indexOf('!') > -1 ) {
    invalid(data, kind.slice(1), error_message);
  } else {
    valid(data, kind, error_message);
  }
}
```



