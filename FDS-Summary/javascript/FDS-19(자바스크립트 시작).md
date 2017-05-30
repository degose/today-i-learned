FDS-19-자바스크립트 시작
========


### <<레벨 테스트>>

- javascript 데이터 유형
    - `Number`
    - `null`
    - `ndefined`
    - `Array`
- 할당 연산자 `=`
    - `>`
    - `!`
    - `<<`
- `Block Scope`
    - `inline` - 자기가 포함한 텍스트까지만 vertical-align 할 수 있다.
    - `block` - 
    - `inline-block` - 
- 보간법(interpolation) : `#{}`
- 에크마 스크립트
- 모던 스크립트
- 예제1 콘솔에 출력되는 값 : true
```js
var book_name = true;
var readBook = function(){
    if(!book_name){
        var book_name = '만들면서 배우는 모던 웹사이트 제작';
    } else {
        book_name = 'Vue.js 완전 정복';
    }
    return book_name;
};
readBook();

console.log('book_name:', book_name);
```
    - var 
    - undifined 는 기본적으로 부정
    - !를 만나면 긍정이 된다.
    - 그런데! 전역변수로 readBook을 불렀잖아, 위에 내용은 지역변수라서 

- 예제2 this가 참조하는 결과 : ??
```js
var f_handles = document.querySelectorAll('.filp-handle');

f_handles.forEach(function(handle){
    nadle.addEventListener('click', filpCard.bind(handle.patentNode));
});

function flipCard() {
    console.log(this);
}
```

### <<몰랐던 단어>>
- 객체지향 : 
- 코어 javascrip : 
- 정적 형지정(static typing)
- 형 검사(strong type checking)
- 클래스의 컴파일-타임 시스템
- 런타임 시스템
- 프로토타입 객체 모델 : 동적 상속을 제공
- HyperTalk
- dBASE
- interpreter(자바스크립트) : 통역 / 해석기(웹브라우저)
- 컴파일 언어 : 하드디스크 작성 / 바로 실행


### <<질문>>
1. JavaScript 언어란? 
    - 가벼운 언어다. 자유롭다.

2. JavaScript 와 JAVA는 다른가?

3. JavaScript 와 ECMAScript 같은 건가?



### <<문법과 타입>>

- 상수(constant) : 값을 가지는 변수이나 그 값을 바꿀 수 없는 변수 / 변수나 상수는 메모리에 할당된 '공간'
- 리터럴(literal) : 변수 및 상수에 저장되는 값 자체 (정수 리터럴, 실수 리터럴, 문자열 리터럴 등등) / 이 공간에 저장되는 '값'
- 자바스크립의 아버지 : 브랜든아이크 

- 문(statement) : 값을 반환하지 않는다.(구문)ex-if문 / for문
- 식(Expression) : 값을 반환한다.(표현식)
- 함수 : 값을 반환한다. return을 하지 않으면 undifined을 반환한다.

- JavaScript 변수(Variable) 선언, 값을 할당
    - 무엇을 변수에 설정하고자 하는가?
    - 오늘 점심은 뭘 먹지?
    ```js
    //변수 선언
    //초기 값은 할당되지 않았다
    var runch; //undefined(가 담겨있다.)

    //선언된 변수에 값을 할당
    //할당하는 역할을 수행하는 연산자 -> 할당(대입) 연산자 `=`
    runch = 김밥;//값: 김밥이라는 이름의 '변수'를 찾아요 -> 참조 오류(Reference Error) 발생
    runch = "김밥";값: 김밥이라는 '문자열 데이터'를 찾아요
    runch = '김밥';//값: 김밥이라는 '문자열 데이터'를 찾아요
    ```
- 실습
```js
var runch;
runch = 'gogi, egg, apple';

var friend;
friend = 'jidori, hyuni, ggoming, arumi, sejeung';
```
- 변수를 선언함과 동시에 값을 할당하는 구문
    ```
    var 변수_이름 = 값;
    var 변수_이름 = 다른_변수_이름; //다른 변수에 할당된 값을 선언하는 변수에도 할당

    var dinner = '치맥'; //점심에 먹은 것을 저녁에도 먹고 싶지 않아!
    var dinner = runch; //점심에 먹은 것을 저녁에도 먹자
    ```
    - 변수에 값을 참조 / 값 복사
- 실습
```js
var dinner = runch;
```

- 변수 이름 작성 규칙
    - 이름은 알아보기 쉽게, 이해하기 쉽게 명시적으로 지어야 한다.
    - 이름은 직관적으로 그것이 무엇을 말하며, 무엇을 행할 수 있는지 알게 지어야 한다.

- 이름 지을 때 하지 말아야 할 것
1. 공백으로 이름이 구분되게 지어서는 안된다.
    - `var my name = 'gose';` [X]
2. 이름을 지을 때 첫 글자가 숫자여서는 안된다.
    - `var 101Team = IoI;` [X]
    - `var 10px = 'Ten Pixel';` [X]
3. 이름을 지을 때 사용하 ㄹ수 있는 특수문자는 정해져 있다.
    - _, $ 을 제외한 다른 특수문자는 사용할 수 없다.
    - `var Team-101 = 'IoI';` [X]
    - `var @design = '디자인 피플'; [X]
4. 대소문자를 구분하는 JavaScript에서는 이름을 지을 때 관례가 있다.
- 어긴다고 해서 문법에 오류가 발생하지는 않지만, 오래 전부터 내려오는 관습이 있다.
    - 변수 이름은 _을 사용하여 이름을 구분한다.
    - 패턴(pattern): 사용 빈도가 높다.

    - Single var pattern : var 변수 선언 키워드를 한 번만 사용하여 변수를 정의하는 패턴
    - `var my_name, is_visible, has_children, remote_control;`

    - 함수 이름은 카멜 케이스(camelCase) 표기법을 사용한다.
    - `getName(), setAge(), showMeTheMoney(), blackSheepWall()`

    - 함수 이름의 첫글자가 대문자인 경우는 특별한 함수일 가능성이 높다.
    - 기본 제공하는 변수와 구분되기도 한다.
    - Navigation(), Tabs(), Carousel(), Component(), ..
    - Vue()

- 변수(식별자(identifier))
    - `var`를 붙이는게 오류가 나지 않는다.
    - `DOCTYPE` 범용적 모드 / 엄격모드???
- Javascript 변수 범위(scope)
    - `전역 변수` (Global Variable)
    - 클라이언트 환경(Front-End)
    - `전역 객체` (Global Object) : Window 객체
    - 전역변수란? 전역 객체의 속성이다.
    - 모든 구역(Block)에서 접근(Access)이 가능한 변수
    ```js
    var type_of_my_phone = 'iPhone';
    console.log('전역 변수:', type_of_my_phone); //iPhone
    ```

    - `지역 변수` (Local Variable)
    - 특정한 구역(Block)에서만 접근이 가능한 변수
    - Block 문
    ```
    {
        var type_of_my_phone = 'Apple Device';
        console.log('블록 내부 변수:', type_of_my_phone);
    }
    console.log('전역 변수는 블록 내부의 변수에 영향을 받았나?:', type_of_my_phone);
    ```

- 호이스팅(Hoisting)
    - 끌어 올리다. 변수가 끌어올려진다.
    ```js
    console.log('is exist variable `somthing`?:', somthing);
    var somthing = '썸씽!';
    ```
    콘솔 뒤에 somthing이 선언되었지만 선언 var something만 끌어올려줘서 undefined로 나온다.

- 상수(Constant): `const`
    - 모두 대문자로 쓰는게 좋다.(변수와 구분 짓는다.)
    - 읽기전용 : 값을 바꿀 수 없다.
    - 고유한 이름 / 한 번 선언된 상수는 재 선언될 수 없다.
    - run타임 / 브라우저 실행중에 / 스크립트가 실행 중에 바꿀 수 없다.
    ```js
    const IS_ROTATION_EARTH = true;
    const is_rotation_earth = true;

    console.log('IS_ROTATION_EARTH:', IS_ROTATION_EARTH)
    console.log('is_rotation_earth:', is_rotation_earth)
    ```
    - 대문자와 소문자를 구분하기 때문에 두가지 다른 상수로 선언된다.

- 데이터 유형(Data Types)
    - ES5 기준
    - 원시 데이터 유형(Primitive Data Types)
        - `undefined` - 부정
        - `null`(부정)
        - `Number` (정수,실수,소수) 0빼고 모든 것이 형이 변환이 됐을때 true / 0, 1
        - `String` (''/" ") 홑따옴표, 쌍따옴표로 묶인 텍스트 '' 공백 문자열 - 부정, ' ' 공백 true
        - `Boolean` true , false , !false(true) , !!false(false)

    - 참조 데이터 유형(Reference Data Types)
        - `Function` : 수행을 위한 절차
        - `Array` : 값의 집합
        - `Object` : 속성의 집합

    - String 문자 유형의 데이터
        - 따옴표(큰,작은)로 묶인 텍스트
        - 사용할 때 유의점
        1. 따옴표의 시작과 끝이 같은 유형이어야 한다.
        2. 문자 데이터 유형을 구분짓기 위한 따옴표가 아닌, 문자로서의 따옴표의 경우는 이스케이스(Escape)처리해야 한다.
        `'나의 하프 마라톤 기록은 50" 23\' 이다.'` / `"나의 하프 마라톤 기록은 50\" 23' 이다."`
        3. 큰 따옴표 사용 시
        `var message_html = "<p class=\"message\" title=\"달리기 기록\">나의 하프마라톤 기록은 50\" 23\'이다.</p>;`
        4. 작은 따옴표 사용 시
        `var message_html = '<p class="message" title="달리기 기록">나의 하프마라톤 기록은 50" 23\'이다.</p>;`

- 데이터 유형 변경(자동) / (유)형 변환
    - 변수를 사용하여 런타임(실시간, 웹 브라우저에서 실행 중인 상황) 중에 값의 유형을 변경할 수 있다.
    - JavaScript는 동적 데이터 유형 처리 언어이기 때문
    - 변수 선언 시에 문자 유형의 테이터 값을 변수에 할당했지만, 웹 브라우저에서 실행 중인 상황에 사용자의 코드에 따라 값의 유형이 바뀔 수 있다.
    ```js
    var process_my_work = '논리에 기반한 선별적 디자인 프로세스';

    process_my_work = false; //문자 -> 불리언으로 변경
    [false]
    process_my_work = function(){}; //불리언 -> 함수로 변경
    [function (){}]
    ```
- 실습
```js
var a, b, c;
// a = [사용자 입력 값];
a = 10;
b = 7;
c = a + c;
[17]

//그런데 사용자가 숫자가 아닌 문자열을 넣을 수도 있다.

a = '십';
b = '칠';
c = a + b;
['십칠']
```

- Single var pattern
```js
var x,y,z;
x = 'x';
y = 'y';
z = 'z';

var x = x = 'x',
        y = 'y',
        z = 'z';
```

- 미리 살펴보는 DOM Script
- DOMScript 에서 Single var pattern을 사용한 예시
```js
var html = window.document.documentElement,
    head = window.document.head,
    body = window.doucment.body;

console.log('html:', html);
console.log('head:', head);
console.log('body:', body);
```

