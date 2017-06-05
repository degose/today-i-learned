FDS-23-함수, 객체지향
========


## << 테스트 >>
- 선언과 관련된 예약어(Reserved keywords)이자, 식별자(Identifier) 이다.
- const는 상수(Constant)를 선언할 때 사용한다.
- var는 변수(Variable)를 선언할 때 사용한다.
- const로 정의하는 상수는 작명 규칙(Naming Convention) 관례에 따라 대문자로만 구성하여 구분할 수 있다.
- var로 정의하는 변수는 대소문자를 섞어 사용 가능하며, 첫글자가 숫자일 경우 오류이다.

## << 오류 유형 >>
- TypeError
- SyntaxError - 문법 오류
- ReferenceError - 선언되지 않은 변수에 접근한 경우 '참조오류'
- InternalError
- RangeError
- permission denied to access property - 권한 없음

### 값 복사
- !!ele - 불리언값
- ["휴대용 선풍기", "여름맞이 샌들"].length : 숫자 2를 반환 (숫자값)
- Math.floor(Math.random()*9) : 숫자 값
- 문자열
- 숫자값

### 값 참조

### if VS switch

### 반복 문에 사용할 수 없는 키워드
- return 은 함수

### for VS for..in
- length속성

### 예시1
```js
{
    var m1 = [1,3,33,333]; //전역변수, 배열
}

var m2 = function(){
    // var m1 = undefined 까지 호이스팅되어서 여기서 해석됨.
    if ((m1 && m1.legth > 0) || !m1) { //m1이 undefined 라서 false || 넘어가서 !m1을 만나서 true가 됨.
        var m1 = new Array(7);//new Array(7)을 쓰면 안된다. undefined가 7개 나온다. [7]이 아니라
    }
    return m1.length;// undefined가 7개 나오니까 7
};

function m3(){ 
    return m2() * m2();// 7 * 7 = 49
}

var final_result = m3();
```

### 예시2
```js
{
    var korAir = {
    name: '코리아 에어',
    location: '대한민국'
};
}
var getKorAirProps = function(){
    for (var property in korAir){ //'코리아 에어'랑 '대한민국'을 순환
        var props = [];
        if(korAir.hasOwnProperty(property)){ //이 객체의 속성이 너 자신의 것이냐? true
            props.push(korAir[property]); //그렇다면 배열 propsd에 korAir 값들을 push 넣어라. 
            // 그래서 props에 '코리아 에어'가 들어가지만 다시 순환되면서 데이터값 초기화된다. 그래서 그다음 '대한민국'이 들어간채 리턴된다.
        }
    }
    return props;
};
var final_result = getKorAirProps();//['대한민국']
```

Q. 참조할때 어떻게? 복사할때 어떻게?




## << 함수 >>

### 함수 선언하기
1. 함수 표현식 (값을 반환) (함수 식(익명함수)을 변수에 할당(대입)) -> 참조
```js
var registerUserInfo = function(){};
```
2. 함수 선언문 (함수에 이름을 붙여서 선언)
```js
function registerUserInfo(){};
```
### 함수 호출하기
- `registerUserInfo();`
- 함수인지 검증 후 실행
- if문을 사용한 예
```js
// isFunction이라는 검증함수에 해당 함수를 검증 받은 뒤 호출
if (isFunction(registerUserInfo)){
    registerUserInfo();
}
```
- 논리 연산자를 사용한 예
- `m1 && m2` : m1이 참이면 m2도 실행
- `m1 || m2` : m1이 거짓이면 m2를 실행
```js
// isFunction(registerUserInfo) 함수의 결과가 참이면(&&) registerUserInfo 함수를 실행
isFunction(registerUserInfo) && registerUserInfo();
```

### 데이터 검증 utils 함수
- `.isNaN(data)`: data값이 숫자가 아니면 true 숫자이면 false
- `Number.isNaN(data)` : 전달된 값이 NaN인지 결정. 오리지널 global isNaN()의 더 강력한 버전.
```js
/**
 * 숫자 유형의 데이터인지 감별하는 유틸리티 함수
 * @global
 * @func isNumber
 * @param {any} data - JavaSript의 모든 데이터 유형
 * @returns {boolean} - 숫자 유형인지 아닌지 유무 true | false
 */
function isNumber(data) {
    return isType(data,'number') && !Number.isNaN(data);
}
/**
 * 함수 유형의 데이터인지 감별하는 유틸리티 함수
 * @global
 * @func isFunction
 * @param {any} data  - JavaScript의 모든 데이터 유형
 * @returns {boolean} - 함수 유형인지 아닌지 유무 true | false
 */
function isFunction(data) {
  return isType(data, 'function');
}
```


### 함수 범위
- 참고 : <http://www.nextree.co.kr/p7363/>
- 영역, Scope
- ES6 이전의 환경에서는 범위는 함수 영역 밖에 존재하지 않는다.
- `스코프 체인(scope chain)`: 함수가 중첩함수일 때 상위함수의 유효범위까지 흡수하는 것. 즉, 하위함수가 실행되는 동안 참조하는 상위 함수의 변수 또는 함수의 메모리를 참조하는 것.
- 전역변수
```js
var g_scope = '전역변수';
```
- 지역변수
```js
function localScope(Prameters){
    console.log('g_scope:',g_scope);// 지역 안에 없으므로 전역변수를 읽는다. '전역변수';
    //함수 안(지역)에서 g_scope를 호출한다면
    //1.변수 영역을 찾고
    //2.Prameters(매개변수)영역을 찾고
    //3.함수를 포함하는 상위 영역을 찾고
    //4.전역변수 영역까지 가서 찾는다.
    //5.그래도 없으면 ReferenceError 발생!

    innerScopeFn();//에러발생 만약 아래를 functionn innerScopeFn(){};으로 쓴다면 전체가 호이스팅 되니까 undefined

    //중첩된 함수 많이 쓰면 안된다.
    var innerScopeFn = function innerScopeFn(params) {
        console.log('l_scope:', l_scope);
        var l_scope = '지역 변수';
    }
}
// 함수 실행
// 전역에서 localScope라는 함수가 실행되었다.
// 전역 변수, 전역 함수 -> 전역 객체의 속성(메서드) 이다.
// window.localScope()
localScope();
```

### this context
- 영역 내 this 변수가 무엇을 참조하나?
- 함수를 누가 실행시켰나?
- 컨텍스트 메뉴(Context menu)
- 전역 함수 정의
```js
function whoCallMe() {
    // this는 자신('this')를 포함하는 함수를 실행시킨 컨텍스트 객체(주체)
    console.log('this:',this);
}
// 명시적 함수 실행
window.whoCallMe(); //this - > window{}

// 암시적 함수 실행 //this - > window{}
whoCallMe();
```
- 객체의 속성(메서드) 정의
```js
var me = {
    whatIsThis: function () {
        console.log('this:',this);
    },
    callMe: whoCallMe //참조 whoCallMe()괄호 쓰면 안된다. 함수를 실행해버려
}
// 명시적 함수(객체.속성(메서드)) - 권장
me.whatIsThis(); // this -> me{}
```

### Arguments(전달인자)와 Parameters(매개변수)
- Parameters(매개변수)
```js
function displayBlockElement(el) {
    // var el = 전달인자;
    // el = <element id = "app"></element>;
    // var를 사용하는 것은 일반 변수
    // 함수의 선언구문 ()괄호 안에 선언된 변수 === 매개변수(parameters) => el
    // 함수 로직
    // 전달 받은 요소의 display 스타일 속성 값을 'block'으로 설정한다.
    el.style.display = 'block';
    // css 속성(2개 이상의 음절로 구분되는)을 적용한 예시
    el.style.borderTopColor = '#4321fe';
    el.style['margin-right']= '1rem'; //margin-right css 표기법을 그대로 써주고 싶다면(JavaScript에서는 -를 읽지 못해서)
}
```
- Arguments(전달인자)
```js
// 함수가 실행될 때,
// 무엇을 전달할 것인가?
// 전달인자(arguments)
displayBlockElement(document.getElementById('app'));// <element id = "app"></element>
```
```js
// 검증
// 전역 함수를 정의
// 명시적 실행
// 암시적 실행을 통해 this가 참조하는 객체가 무엇인지 확인
// 전역에서 this는 무엇을 참조(가리키냐)?
function bigFunc(){
    console.log('this:',this); //window
}
// 객체를 정의
// 객체의 메서드로 이미 정의된 바 있는 전역 함수를 참조 시켜본다.(함수이름 o ,함수이름() x )
// 객체의 메서드를 실행해 봄으로서 this가 참조하는 객체를 확인한다.
var what = {
    who: bigFunc;
}
```

### Arguments(전달인자) 객체
- `arguments` : arguments 객체는 함수에 전달된 인수에 해당하는 Array같은 객체
- 예시 : 수의 합을 반환하는 함수
```js
function sum(n1,n2){
    if(!isNumber(n1) || !isNumber(n2)) {throw '오류'};
    return n1 + n2;
}
function sum(n1,n2,n3,n4,n5){
    // 전달된 인자가 몇 개인지 모를 때?
    // 인자를 집합으로 만들면?
    // 사용자가 전달한 인자들을 집합(Array)의 아이템으로 설정해보세요
    var num_collection = [n1,n2,n3,n4,n5];
    // num_collection.push(n6,n7,n8...);
    
    // length값을 알고 있다면
    // 구문 반복처리
    // for,while,do..while
    if(!isNumber(n1) || !isNimber(n2) || !isNimber(n3) || !isNimber(n4) || !isNimber(n5)){throw '오류'};
    return n1 + n2 + n3 + n4 + n5;

    // 다른 방법
    var l = num_collection.length; // l === 5
    var result = 0;
    while (l--){ // 지금은 5 다음라인부터 4.. 0으로도 처리가 되어야하는데 --l했으면 처리해주지 않는다.
        var n = num_collection[l];//4,3,2,1,0 l만큼 순환한다.
        if(!isNumber(n)) {throw '오류'}
        result += n;
    }
    return result;
}
```
- `arguments`이용
```js
function anotherSum() {
  // 사용자가 함수를 실행할 때, 전달한 인자의 집합 객체를 참조하는 변수 제공
  // 유사 배열(Array like Object): 배열과 비슷
  // 배열처럼 length 속성을 가진다.

  // arguments // [1, 2], [1, 2, 3, 4, 5], [1010, 100, 210, 35, -20]

  for ( var n, k=0, i=0, l=arguments.length; i<l; ++i ) {
    n= arguments[i];
    k += n;
  }
  return k;

  for ( var n=0, i=0, l=arguments.length; i<l; ++i ) {
    n += arguments[i];
  }
  return n;
}

var r1 = anotherSum(1, 2); // 2
var r2 = anotherSum(1, 2, 3, 4, 5); // 5
var r3 = anotherSum(1010, 100, 210, 35, -20); // 5
```
- 그렇다고 argument는 객체가 아니다.
```js
function argumentsObjectIsntArray() {
    // arguments 객체는 유사 배열로 length 속성을 가지지만,
    // 배열의 메서드를 사용할 수는 없다.
    console.log(arguments);
    console.log(arguments.length);
    console.log('arguments.push:',!!arguments.push);
    //arguments.collee();//해당 함수 자신만을 실행 하지만 이렇게 자주 쓰면 안됨
}
argumentsObjectIsntArray();
argumentsObjectIsntArray([9,8,7]);
```
- arguments 객체를 Array로 만들기
```js
/**
 * 유사 배열 객체를 배열 객체로 변경(복사) 처리하여 반환하는 유틸리티 함수
 * 
 * @param {any} o - 유사 배열 객체( 배열과 흡사한 객체 e.g) arguments, NodeList )
 * @returns - (복사된) 배열 객체
 */
function makeArray(o) {//array_like_object
    var array = [];
    if(!('length' in o)){ return [];}// o객체에 length가 없으면 빈 배열을 반환한다. pass
    for (var i=0; i<o.length; i++){
        array.push(o[i]);//array라는 배열에 하나씩 순환하면서 더해진다.
    }
    return array; 
}

// 메서드 빌려쓰기 패턴
function convertArray(o) {
    if(!('length' in o)){ return [];}
    return Array.prototype.slice.call(o); //o한테는 slice 함수가 없기 때문에 Array의 slice를 빌려쓴다.
}
// k라는 배열이 있는데, m이 k 배열을 복사하고싶어. k.slice(0);을 하면 값이 복사가 된다.
```
- 예시
```js
function argumentsConvertArray() {
    var args = makeArray(arguments); //convertArray(), changeArray()
    console.log(!!args.push);//true
}
```

### 재귀(再歸)함수
- 자신을 다시 호출하는 함수
- `arguments.callee` 쓰지마세여 
    - ECMAScript(ES5) 은 엄격 모드에서 arguments.callee()의 사용을 금한다. function 식(expression)에 이름을 주거나 함수 자체를 호출해야 하는 곳에 function 선언을 사용하여 arguments.callee() 사용을 피해야 한다.
    - 일반적인 경우에 인라인 및 tail 재귀를 불가능케 하기에 (tracing 등을 통해 선택한 경우에 그것을 달성할 수 있지만 최고의 코드는 검사가 달리 필요하지 않기에 차선) 다른 주요 문제는 그 재귀 호출이 다른 this 값을 갖는 것입니다. ????뭔소리
- 예시 `팩토리얼(Factorial)` 만들기
- <http://www.mathatube.com/images/factorials.JPG>
- 1! = 1 = 1
- 2! = 2 x 1 = 2
- 5! = 5 x 4 x 3 x 2 x 1 = 120
- 시작한 값을 통해서 순환처리를 할 수 있다.
```js
function factorial(n) {
    if ( n<2 ){return 1;}
    //로직(반복 순환 처리, 조건이 거짓이 나오게 하여 무한 루프에 빠지지 않게 처리)
    // n = 2
    // 원본 값을 기억해주겠다.
    // 재귀 함수가 아닌, 반복문을 활용한 예
    var nn = n; //2
    do {
        nn *= --n;
    } while (n > 1);
    return nn;
    
    // 재귀 함수를 활용한 예
    return n * factorial(--n);
}
factorial(3);
```


### 함수 프로토타입 객체(선언, 할당된 모든 함수객체)가 가진 능력
- `Function.prototype`
- `.call()`
- `.apply()`
- `.bind()`    <- 2009, ES5 (IE 9+)
```js
// Function.prototype {}
console.dir(Function.prototype);
'call' in Function.prototype
```
- 일반적인 함수 실행에서의 this
    - (객체.)함수() // this === 객체
```js
var electric_fan = {
  name: '선풍기',
  on: function(power, time) {
    console.log('this:', this);
    power = power || 1;
    time = time || 1;
    console.log(this.name + '를 파워 '+ power +' 만큼 '+ time +'시간 동안 세게 가동하다');
  },
  off: function() {
    console.log('this:', this);
    console.log(this.name + '를 가동 중지하다');
  },
}
electric_fan.on.call(window, 10,2)
//전지전능한 전역 객체를(window) 10만큼 2시간동안 세게 가동하다
electric_fan.on.apply(window,[10,2])
```

- .call(), .apply() 실행에서의 this
    - this 컨텍스트 객체를 교체(변경)할 수 있다.
    - (객체.)함수.call(컨텍스트 객체, 전달인자(각각 콤마로 구분 전달));
    - (객체.)함수.apply(컨텍스트 객체 전달인자(배열로 묶어서 전달));

- .bind() 에서의 this
    - 상황에 따라서 함수를 바로 실행시키지 않고, 나중에 임의로 실행시켜야 하는 상황
    - this는 컨텍스트 객체를 교체, 전달인자를 2번째 인자 값으로 전달할 수 있다.
    - call() 처럼 콤마로 구분해서 전달해야 하며, 배열로 묶어 전달할 경우, 첫번째 인자로 배열이 전달된다.
    - call, apply 와의 차이점!!!! 바로 실행되지 않는다.
```js
var winPowerTime = electric_fan.on.bind(window);
window.setTimeout(winPowerTime, 3000); //3초 뒤에 실행 (원하는 시점에 실행할 수 있다)
```
