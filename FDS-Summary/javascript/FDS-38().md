FDS-37-AJAX,
========

1. Ajax 란 무엇임 어떻게 생겨났고, 어디에 사용되는지.
- 참고: <https://developer.mozilla.org/ko/docs/AJAX/Getting_Started>
- Ajax란? (Asynchoronous Javascript And XML)

- 비동기 JavaScript

- XMLHttpRequest();

2. Bulma: 간랸한 설명







## AJAX
- 참고: <https://github.com/yamoo9/JJ_CAMP/blob/master/PDF/16%20Javascript%20%EC%BD%94%EC%96%B4-%20AJAX.pdf>
- aria
### 동기 / 비동기
- 동기는 기다렸다 실행
- 비동기는 기다리지 않고 바로 실행
- 
### XHR
### var xhr = new XMLHttpRequest();
- 반드시 new를 사용

### xhr.response

### xhr.status
### send, open
### error 값들
### xhr.onreadystatechange
- 상태가 체인지 되면 이벤트를 실행?
- readystate
- 왜 onload를 사용하지 않고 onreadystatechange를 쓸까?
- 스피너 표시: 예전에는 gif를 사용했고 요즘엔 svg 등등 다양
- <i></i> 아이콘이 아니에여

### cross 
- 포토콜 확인 통신상태 

### 커멘드라인 공부...


### createXHR()
- 확인만 하자.


## 실습
- 라이브 서버 설치
```bash
$ echo '{}' > package.json && npm i -D live-server
```

- 만약 live-server 문제 있다면 -g 글로벌 설치
```bash
$ npm i -g live-server
```

- bulma: <http://bulma.io/>
- <http://bulma.io/documentation/overview/start/>
```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bulma/0.4.2/css/bulma.min.css" />
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
```

- XHR 객체를 생성해야 한다. (생성자 함수를 사용해야 한다.)

## ES6 문법 복습
- let
- const
```js
// 비동기 통신 이벤트 제어 프로그래밍
{
  // Block
  // let, const
  // iife패턴을 쓸 필요가 없다. 그렇지만 아직까지는 iife 패턴을 써주는 것이 좋다.
  let print_btn = document.querySelector('.print-ajax-btn');
  let data_zone = document.querySelector('.data-zone');
  let data_url = './DB/book.txt';
  let renderAjaxData = ()=> {
    xhr = new XMLHttpRequest();
    xhr.onreadystatechange = printAjaxData;
    xhr.open('GET', data_url, true);
    xhr.send(null);
    // console.log(this); // window가 될 수 있으므로 수시로 this를 확인해줘야함

    // 클릭 후, 비활성화 ( 두 가지 방법 )
    print_btn.removeEventListener('click', renderAjaxData, true);
    // print_btn.setAttribute('disabled','disabled');
  };
  let printAjaxData = ()=> {
    if ( xhr.status === 200 && xhr.readyState === 4 ) {
      data_zone.innerHTML = xhr.responseText;
    } else {
      data_zone.innerHTML = '통신에 실패했습니다. :('
    }
  };
  // renderAjaxData.bind(print_btn) this를 지정해야 할 경우
  print_btn.addEventListener('click', renderAjaxData, true);
}

```

## xml 랜덤 데이터 가져오기
- curl 명령어
```bash
$ curl https://randomuser.me/api/\?results\=10\&format\=xml > DB/user.xml
```
```bash
$ curl https://randomuser.me/api\?results\=10 > DB/user.json
```

## json