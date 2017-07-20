FDS-47-인스턴스,메서드,렌더링,디렉티브
========


## 배열 요소 제어할 때
```js
app
app.components
app.components.push('off canvas menu');

var data = [1,2,3,4]

data[data.length] = 102 
// 각 괄호 표기법

app.components[app.components.length] = 'air pressor'
// 이런 방법은 접근성이 없기 때문에 사용하지 말자
```


## root 요소


## template 
- 묶음 조각인데 묶어놓고 사라지기때문에 문법오류가 나지 않는다.
- 

## defineProperty
- const 를 쓰는 이유?
- 상수로서 쉽게 지우지 못하게 된다.
```js
const fds {};
{
  let name = '';
  let notify = function( msg ) { console.log(msg);};
  Object.defineProperty(fds, 'name', {
    get: function () {
      return name;
    },
    set: function () {
      notify('update value:', v);
      name v;
    }
  });
}
```

## 반응형 시스템


## 인스턴스
- 라이프사이클훅
- 메서드
- 조건부 렌더링
- v-if, v-else, v-esle-if, v-show
- 리스트 렌더링
- v-for 객체, 배열, 숫자, 문자
- v-for="alias in(of) data"
- v-for="(alias,index) in(of) array"
- v-for="(value,key,index) in(of) object"
- 디렉티브
- v-text, v-html, v-once, v-cloak

