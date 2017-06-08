# JavaScript기초복습-1
- 참고 : MDN, fds 프리스쿨 자료

## 함수 구문
```js
new Function ([arg1[, arg2[, ...argN]],] functionBody)
```
### 매개변수
- arg1, arg2, ... argN
- 형식 인수(argument)명으로 함수에 의해 사용되는 이름. 각각은 유효한 JavaScript 식별자(identifier)와 대응하는 문자열 또는 쉼표로 구분된 그런 문자열 목록이어야 한다. 즉 예를 들어 "x", "theValue" 또는 "a,b".
- functionBody
- 함수 정의를 이루는 JavaScript 문(statement)을 포함하는 문자열.

## 중첩된 함수와 클로저
- 내부 함수는 외부 함수문에서 액세스할 수 있다.
- 내부 함수를 형성하는 클로저: 외부 함수는 내부 함수의 인수와 변수를 사용할 수 없는 반면에 내부 함수는 외부 함수의 인수와 변수를 사용할 수 있습니다.
```js
function outside(x) {
  function inside(y) {
    return x + y;
  }
  return inside;
}
fn_inside = outside(3); // Think of it like: give me a function that adds 3 to whatever you give it
result = fn_inside(5); // returns 8

result1 = outside(3)(5); // returns 8
```

## 인수 객체 사용하기
- `arguments[i]`
- 배열을 닮은것이지 배열이 아니다.
```js
function myConcat(separator) {
   var result = "", // initialize list
       i;
   // iterate through arguments
   for (i = 1; i < arguments.length; i++) {
      result += arguments[i] + separator;
   }
   return result;
}
// returns "red, orange, blue, "
myConcat(", ", "red", "orange", "blue");

// returns "elephant; giraffe; lion; cheetah; "
myConcat("; ", "elephant", "giraffe", "lion", "cheetah");

// returns "sage. basil. oregano. pepper. parsley. "
myConcat(". ", "sage", "basil", "oregano", "pepper", "parsley");
```






<< 함수 해석하기 >>
```js
function map(f,a) {
  var result = [], // Create a new Array
      i;
  for (i = 0; i != a.length; i++)
    result[i] = f(a[i]);
  return result;
}

var multiply = function(x) { return x * x * x; }; // Expression function.
map(multiply, [0, 1, 2, 5, 10]); //  [0, 1, 8, 125, 1000]
```

- 이 코드는 왜 실행되지 않을까?
    왜냐면 변수는 undefined로 호출되기 때문에 undefined를 실행하면 에러가 뜬다. 
    만약 선언문으로 호출하면 전체가 호이스팅 되니까 실행된다.
```js
console.log(square(5));
square = function (n) {
  return n * n;
}
```


```js
function factorial(n){
  if ((n == 0) || (n == 1))
    return 1;
  else
    return (n * factorial(n - 1));
}

var a, b, c, d, e;
a = factorial(1); // a gets the value 1
b = factorial(2); // b gets the value 2
c = factorial(3); // c gets the value 6
d = factorial(4); // d gets the value 24 -> 4 * (3,2,1 순환) * 3 * 2 * 1 = 24
e = factorial(5); // e gets the value 120 -> 5 * 4 * 3 * 2 * 1 = 120
```

- 재귀함수, 스택형 동작
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/%ED%95%A8%EC%88%98#Recursion
```js
function foo(i) {
  if (i < 0){
    return;
  }
  console.log('begin:' + i);
  foo(i - 1);
  console.log('end:' + i);
}
foo(3);

// Output:

// begin:3
// begin:2
// begin:1
// begin:0
// end:0
// end:1 -> 여기서 -1 이 나와야할 거 같은데 왜 1이 됬을까? => 위에 if문은 -1이 됐을때 끝났고. 재귀함수를 하느라 남아있던 0,1,2,3이 실행되면서 콘솔로 찍히게된다.
// end:2
// end:3
```