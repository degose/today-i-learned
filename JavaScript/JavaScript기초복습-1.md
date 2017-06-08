# JavaScript기초복습-1
- 참고 : MDN, fds 프리스쿨 자료

## 변수(식별자 'Identifier')
### 변수 선언
- 변수를 `선언` (var 식별자)
- 값을 `할당` (var 식별자 = 값;)
- 값을 저장할때 사용하는 식별자, 모든 자료형을 담아둘 수 있다.
- 하나의 값만을 가진다. 재할당하는 경우 -> 마지막에 할당된 값 적용
- var를 붙이지 않으면 전역변수로 선언 -> strict mode에서 error발생.(사용하지마)
### 변수 평가
- (var a;)지정된 초기값 없이 선언된 변수의 값 -> `undefined`를 갖는다.
- 선언되지 않은 변수에 접근을 시도하면 -> `ReferenceError`
- `undefined`
    - boolean 문맥에서 `false` 
    - 수치 문맥에서 `NaN(숫자가 아닌 값)`
- `null`
    - 비어있음을 명시적으로 표현
    - boolean 문맥에서 `false`
    - 수치 문맥에서 `0`
### 변수 호이스팅
- 호이스팅 된 변수의 값은 undefined 반환
- 심지어 이 변수를 사용 혹은 참조한 후에 선언 및 초기화하더라도 undefined 반환
- 함수 내의 모든 var 문은 가능하면 함수 최 상단 근처에 두는 것이 좋다.

## 데이터 구조 및 형
- 객체 : 값을 위한 컨테이너
- 함수 : 어플리케이션이 수행할 수 있는 절차

### 데이터 형 변환
- 동적 형지정(정형) 언어 : 변수를 선언할 때 형 지정을 따로 하지 않아도 된다. 그리고 데이터 형이 스크립트 실행(런타임) 도중 필요에 의해 자동으로 변환됨.
#### 문자열을 숫자로 변환
- 숫자를 나타내는 값이 문자열로 메모리에 있는 경우, 변환을 위한 메서드
- `parseInt()`
    - 오직 정수(딱 떨어지는 수 e.g)123)만 반환. 소수(소수점이 붙는 수e.g)12.3)에서는 사용성이 떨어진다.
    - 진법(Radix)매개변수를 포함해야 한다.->??????
- `parseFloat()`
    - 문자열을 부동소수점(floating point number)로 변환 (`"abc" -> Returns NaN / "1.2abc" -> Returns 1.2`)
- `+(단항 더하기) 연산자`
```js
"1.1" + "1.1" = "1.11.1" // "String" + "String" = "StringString" // 문자열
(+"1.1") + (+"1.1") = 2.2 // +(단항 연산자)를 이용하여 숫자열로 반환
```


## 반복문
### 예외처리문
#### throw
#### try...catch
<https://goo.gl/7q2TxS>






## 표현식 vs 문
### 표현식
- 값을 반환 하는 간단한 코드
```js
412
1 + 2
'fastcampus'
```
### 문
- 세미콜론(;)으로 끝나는 식 (값을 반환하지 않음)
```js
413;
var school = 'fastcampus'
'fastcampus';
```

## 삼항 조건 연산자
(불표현식) ? (참일 때 실행하는 문장) : (거짓일때 실행하는 문장)
```js
var input = prompt('숫자를 입력해주세요','');
var number = Number(input);

(number > 0) ? alert('양수입니다.') : alert('음수입니다.');
// 
```


property
아직 잘 모르는 부분 메모

반복문
[]순환??
data[direction](item); //이거 왜 이렇게 쓴다고?
this 
context 
arguments 
parameters 
재귀함수 
bind 
call 
apply