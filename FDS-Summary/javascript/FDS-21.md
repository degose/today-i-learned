FDS-21-
========

### << 액티비티 테스트 >>
#### <<참조가 되는 데이터 유형>>
- Object `var glass = {};`
- Array `var glasses = [];`
- Function `var watchGlass = function(){};`
#### <<Constructor로 판별할 수 있는 type>>
- Object , Array, Number, String
#### <<배열>>
```js
var arr = [2,7,5,8];

arr.length => 4
arr[3] => 8
typeof arr => Array //오답
arr.push(9) => arr = [2,7,5,8,9];
arr.unshift(4) => arr = [4,2,5,8];
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
var c = a++; //
var c = ++a;
var c = b;
var c = b--;
var c = --a+b;
```
```js
1 =='1' //true
typeof null == typeof Array() //
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