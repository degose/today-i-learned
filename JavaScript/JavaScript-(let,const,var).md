## ES6의 let, const 그리고 var

### var 의 단점
- ES5에서 변수를 선언할 수 있는 유일한 방법인 var
- 변하지 않는 상수를 선언하고 싶다면 `var ABC = ABC;`라고 규칙을 정해 사용할 수 있지만 사실상 값을 변화시킬 수 있다.
- fucntion-level-scope -> 함수 구문 내에서 선언된 변수는 함수 코드 블럭 내에서만 유효하고 함수 밖에서는 유효하지않다.(참조할 수 없다.)
- 전역 변수의 남발
- var 키워드 생략 허용 -> 의도하지 않은 변수의 전역화
- 중복 선언 허용 -> 의도하지 않은 변수값 변경
- 변수 호이스팅 -> 변수를 선언하기 전에 참조가 가능하다.
```javascript
// 전역변수
var x = 0;

// 블록 스코프
{
  var x = 1;
  console.log(x); // 1
}
console.log(x); // 1

// 함수 스코프 var를 생략하면 전역변수 x를 찾는다.
function test() {
  x = 2;
  console.log(x); // 2
}
test();
console.log(x) // 2

fucntion test2() {
  // 지역 변수
  var x = 3;
  console.log(x); // 3
}
test2();
console.log(x); // 2

// 호이스팅
console.log(foo); // Undefined(에러가 아님)
var foo;
```
- var를 이용한 전역 변수는 유효범위가 넓어서 어디에서 어떻게 사용될것인지 파악하기 힘들어 의도하지 않게 변경될 수 있어 복잡성을 증가 시킨다.

### Block-level-scope
- 코드 블럭 내에서 선언된 변수는 코드 블럭 내에서만 유효하며 코드 블럭 외부에서는 참조할 수 없다.

### let
- block-level scope를 갖는다.
- 중복선언 시 syntax error 발생
- var보다 직관적이다.
- `window.변수`를 찍으면 undefined를 반환한다. let으로 선언된 변수는 보이지 않는 블록으로 감싸져 있기 때문
```javascript
let y = 0;
{
  let y = 1;
  let z = 1;
}
console.log(y); // 0;
console.log(z); // z is not defined

let y = 2; // syntax Error

// 호이스팅
console.log(bar); // ReferenceError : bar is not defined
let bar;
```

### const
- 변하지않는 값 상수를 선언할 때 사용한다.
- 선언과 동시에 초기화가 이루어져야 한다.
```javascript
const a = 1;
a = 2; // TypeError: Assingment to constant variable

const b; // SyntaxError: Missing initializer in const declaration
```
- const로 선언된 상수는 재할당이 불가능 하다.
- 재할당은 불가능하지만 할당된 객체의 내용은 변경할 수 있다.
- 객체 타입 변수 선언을 할 시에 유용하다.
```javascript
const me = {
  name: 'ko',
};
me.name = 'se';
console.log(me); // {name: 'se'}
```
