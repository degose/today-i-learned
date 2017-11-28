## Ajax

* http://wherethelightis.tistory.com/14
* Asynchronos Javascript And XML
* 자바스크립트를 통해서 서버에 데이터를 요청하는 것이다. HTML form 태그가 아니라 자바스크립트를 통해서! 따라서 우리는 서버에서 로딩된 데이터를 페이지에 보여주기 위해 새로운 HTML페이지로 갈 필요도 없고 '새로고침'을 할 필요가 없는 것이다. 부분 부분만 로딩되므로 속도가 빠르다.
* 비동기적이라는 의미는 클라이언트에서 서버에 요청을 보낼 때 요청을 보내놓고 프로그램은 계속 돌아간다는 의미
* 먼저 요청한 것에 대한 콜백1 함수가 먼저 실행되지 않는다는 것이다.
* 새로고침 없이 수행되는 비동기성 사용자의 Event가 있으면 전체 페이지가 아닌 일부분만 업데이트 할 수 있게 해준다.
* 페이지 일부분을 업데이트 하기 위한 정보를 서버에 요청할 수 있다.
* 서버로부터 받은 데이터로 작업을 한다.
* 뷰와 리액트는 ajax를 통해 하는데 그럼 전통적인 웹에서는 어떻게 하나??
  * PHP, JSP 같은 서버 사이드 프로그래밍 언어의 Form 전송이나 페이지 로드를 통한 전송방식

### XMLHttpRequest
- Ajax로 실행되는 HTTP 통신은 XMLHttpREquest규격을 이용하고 있다.
- Ajax 는 XHR객체를 형성하고 이 객체의 콜백을 만들고 HTML 메소드와 url을 결정한뒤 XHR 객체의 메소드로 정보를 보내는 방식
- 첫번째 파라미터 : HTTP method - GET, POST, HEAD 등(꼭 대분자로 표기-> 특정 브라우저에서 처리하지 않을 수도 있다.)
- 두번째 파라미터 : 요구할 페이지의 URL 
- 세번째 파라미터 : 비동기식으로 수행될지 결정
```javascript
var httpRequest = new XMLHttpRequest();
// 새로운 객체 생성
httpRequest.onreadystatementchange = nameOfTheFucntion;
httpRequest.onreadystatementchange = function(){
  // process the server response
}
httpRequest.open('GET', 'http://url.file', true);
httpRequest.send(null);
```

### 장점
- 페이지 이동없이 고속으로 화면을 전환할 수 있다.
- 서버처리를 기다리지 않고 비동기 요청이 가능하다.
- 수신하는 데이터 양을 줄일 수 있고, 클라이언트에게 처리를 위임할 수도 있다.

### 단점
- 서버를 통한 통신은 새로고침이 되기 때문에 페이지가 다시 그려지기 때문에 사용자가 변화되는 것을 감지할 수 있지만, ajax를 통한 비동기 통신을 할 시에는 부분만 바뀌기 때문에 사용자가 변화를 감지하기가 힘들다. 그러기 때문에 레이지 로딩이나 스피너 같은 요소를 추가하여 사용자 UX적인 부분을 추가해주어야 한다.
- Ajax를 쓸 수 없는 브라우저에 대한 문제
- Http 클라이언트의 기능이 한정되어 있다.
- 페이지 이동없는 통신으로 인한 보안상의 문제
- 지원하는 Charset이 한청되어 있다.
- 스크립트로 작성되므로 Debugging이 용이하지 않다.
- 요청을 남발하면 역으로 서버에 부하가 늘 수 있다.
- 동일-출처 정책으로 인해 다른 도메인과는 통신이 불가능하다
  - https://brunch.co.kr/@adrenalinee31/1