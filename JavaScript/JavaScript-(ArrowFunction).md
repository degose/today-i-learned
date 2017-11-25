## 화살표 함수

- function 키워드 대신 화살표`(=>)`를 사용하여 함수를 선언할 수 있다.
- 익명 함수로만 사용할 수 있다. -> Arrow function을 호출하려면 함수 표현식을 사용한다.
```javascript
const a = x => x * x;
console.log(a(10)); // 100;

var a = function(x) {
  return x * x;
};
```
- 콜백함수로 사용할 수 있다.
```javascript
const arr = [1,2,3];
const pow = arr.map(x => x * x);
console.log(pow); // [1,4,9]
```
- 화살표 함수에서는 arguments(함수 호출 시 전달된 인수의 정보를 담고 있는 유사배열 객체) 프로퍼티가 없다. 가변인자함수의 경우 인수를 전달받는 것이 불가능하므로 이 arguments 객체를 활용할 수 있다.
- 대신 rest 파라미터`...rest`를 사용하여 가변인자를 함수 내부에 배열로 전달할 수 있다.
- ES5의 this는 생성자 함수와 객체의 메소드를 제외한 모든 함수(내부함수, 콜백함수 등)의 내부 this는 전역객체 window를 가리킨다.
- Arrow function은 언제나 자신을 포함하는 외부 scope에서 this를 계승 받는다.
- 자신만의 this를 생성하지 않고 자신을 포함하고 있는 컨텍스트로부터 this를 계승 받는다. Lexical this
- 메소드 정의 시 사용하지 말자.
- prototype에 Arrow function 메소드를 할당하지 말자
- 생성자 함수로 사용할 수 없다.
- addEventListener 함수의 콜백함수로 사용하지 말자
