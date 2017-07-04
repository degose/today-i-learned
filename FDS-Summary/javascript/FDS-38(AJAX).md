FDS-37-AJAX
========

## Ajax
- 참고: <https://developer.mozilla.org/ko/docs/AJAX/Getting_Started>
- 참고: <https://github.com/yamoo9/JJ_CAMP/blob/master/PDF/16%20Javascript%20%EC%BD%94%EC%96%B4-%20AJAX.pdf>
- 참고: <http://visualize.tistory.com/402>
- Ajax란? (Asynchoronous Javascript And XML)
  - 서버로부터 데이터를 가져와 전체 페이지를 새로고침하지 않고 일부만 로드할 수 있게 하는 기법을 말한다.
  - 비동기적 자바스크립트와 XML로 브라우저 내에서 비동기 기능을 제공하는 모든 기법을 통칭한다.
  - 전통적인 웹에서는 웹서버에서 데이터를 처리한 후 HTML로 작성하지만 AJAX에서는 필요한 데이터만 XML같은 가벼운 형식의 데이터로 전송한다.
  - ajax를 이용한 시스템의 예 -> 검색창 연관검색어 & 자동완성, 메일 추가 & 삭제, 장바구니 추가, 회원가입 중복아이디 여부 표시 등
### Ajax 동작방식
  1. 요청: 브라우저가 서버에 데이터를 요청하면(XMLHttpRequest 객체를 이용) -> 서버는 응답으로 데이터를 처리한다.(주로 HTML, XML, JSON형식)
  ```js
  var xhr = new XMLHttpRequest(); // new 생성자표현식으로 생성
  xhr.open('GET','data.json',true); // 매개변수: 'HTML메서드','요청을 처리할 페이지 URL', 비동기(true) or 동기(false)
  xhr.send(null); // 서버로 전달, 추가정보가 전달되지 않으면 null 사용
  ```
  2. 응답: 서버가 응답을 완료하면 -> 브라우저에서는 이벤트가 발생 -> 데이터를 처리하면 페이지의 일부가 변환되는 자바스크립트 호출
  ```js
  xhr.onload = function(){
    if( xhr.status === 200 ) { // xhr객체의 status속성값을 검사하여 서버의 응답이 정상인지를 확인
      // code
    }
  }
  ```
### 데이터 형식
  - XML
    - 태그로 속성과 데이터를 구분. 가독성은 좋으나 용량이 크고 데이터가 많아지면 분석속도가 떨어진다.
    - 실 데이터가 아닌 tag글자이며 배열형식이나 반복구조의 경우 불필요한 데이터가 계속 해서 나타난다.
  ```xml
  <user>
	<results>
		<gender>female</gender>
		<name>
			<title>miss</title>
			<first>pia</first>
			<last>ludwig</last>
		</name>
  </user>
  ```
  - JSON
    - JavaScript의 객체 형태로 데이터를 전송하는 형식. 가독성이 좋고 용량이 적으며 가장 많이 쓰인다.
  ```json
  {
    "items": [
      {
        "key": "First",
        "value": 100
      },{
        "key": "Last",
        "value": "Mixed"
      }
    ],
    "obj": {
      "number": 1.2345e-6,
      "enabled": true
    },
    "message": "Strings have to be in double-quotes."
  }
  ```
### 동기 / 비동기
- 동기는 기다렸다 실행
- 비동기는 기다리지 않고 바로 실행
### State
- 서버의 처리 결과
  - 200 : 서버가 응답을 완료했으며, 아무런 문제가 없다.
  - 304 : 응답 내용이 이전 응답 내용과 동일하다.
  - 404 : 페이지를 찾을 수 없다.
  - 500 : 서버 내부에서 오류가 발생했다.
### onreadystatechange
- 서버의 처리상태의 변화에 따른 이벤트 발생 처리 상태 값을 readyState 프로퍼티로 제공
- readyState가 변할 때마다 호출되는 콜백 함수
- 왜 onload를 사용하지 않고 onreadystatechange를 쓸까?
  - 0 (uninitialized)
  - 1 (loading)
  - 2 (loaded)
  - 3 (interactive)
  - 4 (complete)
### responseText
- 텍스트형태로 데이터 리턴
### responseXML
- XML형태로 데이터 리턴
### createXHR
- 확인만 하자.
- xhr 객체를 IE6 이하는 지원하지 않는다.


## Bulma
- 참고: <http://bulma.io/>
- Flexbox를 사용하여 반응형 웹사이트를 제작할 수 있는 Modern CSS 프레임워크. 
- Bootstrap 과 달리 간단한 클래스명만으로도 반응형 구조를 만들 수 있다. 
- Flex 속성을 사용하기 때문에 크롬, 사파리, 파이어폭스, 오페라, 익스플로러10+에서만 사용할 수 있다.
```html
<head>
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bulma/0.4.0/css/bulma.css">
  <!-- link로 불러온다. -->
</head>
<body>
  <!-- 클래스 명으로 grid 구현 -->
  <div class="columns is-mobile">
  <div class="column is-half is-offset-one-quarter"></div>
</body>
```



## 실습
- 라이브 서버 설치
```bash
$ echo '{}' > package.json && npm i -D live-server
```
- 만약 live-server 문제 있다면 -g 글로벌 설치
```bash
$ npm i -g live-server
```

## xml, json 랜덤 데이터 가져오기
- 참고: <https://www.lesstif.com/pages/viewpage.action?pageId=14745703>
- curl 명령어
```bash
$ curl https://randomuser.me/api/\?results\=10\&format\=xml > DB/user.xml
```
```bash
$ curl https://randomuser.me/api\?results\=10 > DB/user.json
```

## ES6 문법 복습
- let: 재할당이 필요한 변수. 블록스코프레벨을 갖는다.
- 백틱(`): 문자열 삽입
- 화살표 함수 `x => {}`: 익명 함수, 콜백 함수로 사용할 수 있다. 
  ```js
  var pow = function (x) { return x * x; };
  var pow = x => x * x;
  ```
- ${n} 표현식: 문자열로 자동변환
  ```js
  <td class="td name">${user.name}</td>
  ```