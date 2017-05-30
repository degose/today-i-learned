FDS-20-참조 유형의 데이터 / 
========

### <<몰랐던 단어>>




### << JavaScript 데이터 유형>>

#### <<변수 선언, 값 할당>>
- 상수 변수와 유사하지만, 한번만 선언, 값 할당

#### <<원시 유형의 데이터>>
- Number
`var num = 291029384;`
- String
`var str = 'morning food';`
- Boolean
`var boo = false;`
- null
`const NULL = null;`
- undefined
`const UNDEFINED = undefined;`





#### <<참조 유형의 데이터>>
- Object
```js
var glass = {}; //new Object()
```
- Function
```js
var watchGlass = function(){}; //new Function()
```
- Array
```js
var glasses = []; //new Array()
```


### <<JavaScript 데이터 형 변환>>
- 숫자 데이터 - 문자 데이터로 변경되는 사례
```js
console.log('num:', num);
```
- String(숫자데이터) => "문자데이터"
    ```js
    var convert_num_to_str_case1 = String(num);
    console.log('String(num):', convert_num_to_str_case1);
    console.log('String(num):', typeof convert_num_to_str_case1);
    ```
- 숫자데이터 + '' => "문자데이터"
    ```js
    var convert_num_to_str_case2 = num + '';
    console.log('num + \'\':', convert_num_to_str_case2);
    console.log('num + \'\':', typeof convert_num_to_str_case2);
    ```
- 숫자데이터.toString() => "문자데이터"
    ```js
    var convert_num_to_str_case3 = num.toString();
    console.log('num.toString():', convert_num_to_str_case3);
    console.log('num.toString():', typeof convert_num_to_str_case3);
    ```

- `typeof` : 뒤에 오는 값의 유형을 나타냄



### <<문자 데이터 - 숫자 데이터로 변경되는 사례>>
1. Number(문자데이터(숫자형)) 함수 e.g) "23512"
2. -, *, /, % => '123451' - 0 = 123451
3. +문자데이터(숫자형) => 숫자데이터 e.g) +"23512"

### <<문자 데이터(숫자 + 문자를 포함하는 문자) - 숫자 데이터로 변경되는 사례>>
- 콘솔창에서 그룹짓기
```js
console.group('문자 데이터(숫자 + 문자를 포함하는 문자) - 숫자 데이터로 변경되는 사례');
console.groupEnd('문자 데이터(숫자 + 문자를 포함하는 문자) - 숫자 데이터로 변경되는 사례');
```
```js
var news_font_size = '16.23px';
```
- JavaScript 내장 함수
- `window.parseInt()`(단위를포함하는문자, 10) <= 단위를 제거하고 정수 값 반환
```js
var convert_news_font_size_to_int = window.parseInt(news_font_size, 10);
console.log('convert_news_font_size_to_int:', convert_news_font_size_to_int); //16
```
- `window.parseFloat()`(단위를포함하는문자, 10) <=단위를 제거하고 실수 값 반환
```js
var convert_news_font_size_to_float = window.parseFloat(news_font_size, 10);
console.log('convert_news_font_size_to_float:', convert_news_font_size_to_float); //16.23
```


### <<데이터 => 불리언 데이터로 변경되는 사례>>
1. `Boolean` (데이터) 함수 => 불리언 데이터로 변경
```js
console.log('Boolean(num):', Boolean(num));
console.log('Boolean(0):', Boolean(0)); // 0은 false 로 변경
console.log('Boolean(str):', Boolean(str)); // 공백문자 ''은 false 로 변경
console.log('Boolean(''):', Boolean(''));
console.log('Boolean(' '):', Boolean(' ')); // ' ' 은 true로 변경
console.log('Boolean(glasses):', Boolean(glasses));
console.log('Boolean(glass):', Boolean(glass));
console.log('Boolean(watchGlass):', Boolean(watchGlass));
```
- 구분자를 넣고 싶을때
```js
console.log('%c---------------','color: #2367fc'); // 구분자
```
2. `!!` (부정의 부정 === 긍정) => 불리언 데이터로 변경
```js
console.log('!!num:', !!num);
console.log('!!0:',!!0); // 0은 false 로 변경
console.log('!!str:', !!str); // 공백문자 ''은 false 로 변경
console.log('!!'':', !!'');
console.log('!!' ':', !!' '); // ' ' 은 true로 변경
console.log('!!glass:', !!glass);
console.log('!!glasses:', !!glasses);
console.log('!!watchGlass:', !!watchGlass);
```

<< null, undefined 형 변환 체크 >>

- `!!`
```js
console.log('!!null:', !!null);
console.log('!!undefined:', !!undefined);
```
- `!`
```js
console.log('!null:', !null);
console.log('!undefined:', !undefined);
```
- `+ ''`
```js
console.log('null + \'\':', null + '');
console.log('typeof (null + \'\'):', typeof (null + ''));
console.log('undefined + \'\':', null + '');
console.log('typeof (undefined + \'\':)', typeof (undefined + '');
```



### <<리터럴>>

#### <<JavaScript 에서 객체를 생성하는 정식 구문>>
```js
var minimum = new Number(10);
console.log('minimum:', );
```


### <<값 복사(pass by value)>>
- 값 복사가 이루어지는 데이터 유형
- 원시 데이터 유형
- `number, string, boolean, null, undefined`

- 변수 n1을 선언한 후, 값으로 숫자 리터럴(값) 99를 할당한다.
- 변수 n1을 선언한 수, 숫자 값 99를 변수 n1에 복사한다.
- 
```js
var n1 = 99;
//변수 k2를 선언한 후, n1 변수에 복사된 숫자 값 99를 복사한다.
var k2 = n1;
```
- n1, k2에 복사된 숫자 데이터는 같은 값으로 보이나, 서로 다른 값이다.
- n1의 데이터 값을 변경했을 때, k2는 변화가 없어야 한다.
```js
n1 = n1 * n1;
console.log('n1:',n1);
console.log('k2:',k2);
```


### <<값 참조(pass by reference)>>
- 값 참조가 이루어지는 데이터 유형
- 참조형 데이터 유형
- ??? 함수
- 원래 값이 바뀌면 참조한 값도 바뀐다.

```js
var playlist = music_list;

console.log('music_list');
console.log('playlist');

playlist.push('루키');

music_list.author = 'mike';
```


### <<함수객체 (Function Object)>>

- 함수 생성자를 통해 함수 객체를 생성
```js
var myFn = new Function('console.log("create function object from function constructor.")');
```

- 함수 선언문: 함수 이름 선언
```js
function doIt(){}
function going(){}
console.log('do it!');

doIt();
sendMail();
```
- 함수 표현식: 변쉥 함수 표현식(함수 리터럴)을 할당
```js
var sendMail = function(){};
var showMe = function(){};
```

- 함수 선언문과 함수 표현식. 그리고 호이스팅(Hoisting)
- 함수선언문은 선언문 통째가 위로 올라간다.
- 그렇지만 오류가 나는 함수 표현식을 쓰는 습관이 좋다.(애초에 함수와 변수를 위에 선언하고 써라va)

### <<기본객체 (Plain Object)>>
- `속성(key): 값(value)` 쌍(Pair)으로 구성된 집합체(데이터 덩어리)

```js
var init_style_of_body = {
    'margin'     : 0,
    'font-size'  : '14px',
    lineHeight   : 1.5,
    letterSpacing: 0.04 + 'em',
    color        : '#313233'
};
init_style_of_body.color
#313233
init_style_of_body["font-size"]
"14px"
```
- 변수
```js
var legs = 4;
```

- 객체의 속성(변수)
```js
var animal = {};
animal.legs = 4;
```

- 객체의 리터럴 속성을 출력하는 방법
```js
var circle = 8;
var 
var gotMaker
var superCar = {
    engine: 'V8',
    maker: 'KIA'
};
```

- 객체의 속성을 제거할 수 있나?
- delete 객체.속성;
- 전역객체인 window 객체의 속성은 제거할 수 없다.
- 전역을 오염시키는 행위는 안티 패턴이다.
- 전역에 변수를 많이 만들지 말라.
- 비울 수 있다. : null & indefined
