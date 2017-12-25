# 클라이언트-서버 통신 및 데이터
========

## RESTful하다의 의미
* HTTP 프로토콜을 정확히 의도에 맞게 활용하여 디자인하였을 때 RESTful 하다라고 말한다.
* HTTP URI 자원을 HTTP 메서드로 잘 정의된 설계
* 왜 RESTful 하게?
    * 잘 디자인 된 API는 서비스가 여러 플랫폼을 지원해야 할 때, 혹은 API로서 공개되어야 할 때, 설명을 간결하게 해주며 여러가지 문제 상황을 해결하기 때문에.
* REST의 기본 원칙을 성실히 지킨 서비스 디자인

## RESTful API
- 참고: <https://spoqa.github.io/2013/06/11/more-restful-interface.html>
- 참고: <http://blog.naver.com/PostView.nhn?blogId=complusblog&logNo=220986337770>
- REST(Representatianal State Transfer) 
### 정의
- 자원(RESOURCE) - URI
  - xml, json 문서 파일, jpg 이미지, mp4 음악파일 등
  - URI(Uniform Resource Identifier) 통합 자원 식별자, 특정 자원의 위치를 나타내는 유일한 주소(url은 uri의 한 종류)
- 행위(Verb) - HTTP METHOD
  - rest API에서 다루는 모든 리소스는 문서, 이미지, 음악 파일에 상관없이 같은 메소드에 의해 다뤄진다.
  - GET
  - POST: 파라미터 정보를 헤더나 바디에 포함시킬 수 있다.
  - PUT
  - DELETE
- 표현(Representations)
  - URI는 정보의 자원을 표현해야 한다.
  - 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현한다.
- '무엇을(HTTP URI로 정의된 리소스) 어떻게 한다(HTTP Method + Payload)'
### 특징
- Uniform(유니폼 인터페이스) : 이미지든 문서든 리소스에 대한 처리가 일관된 형태로 요청된다.(동일한 API 메소드를 갖는다.)
- Stateless(상태 없음) : API를 제공하는 서버측에서 문맥을 저장하지 않는다. 세션 정보등을 서버에서 유지하지 않고 클라이언트가 자체적으로 관리.
- Casheable(캐시 가능) : 같은 URI에 대한 요청이 여러번 있을 때, URI 리소스를 매번 서버로 요청하지 않고, 클라이언트 HTTP 캐시에서 미리 가져온 정보를 반환한다.
- Self-descriptveness(자체 표현 구조) : API 메세지 자체로 쉽게 이해할 수 있어야하고, 별도의 주석, 문서 없이도 원하는 바를 쉽게 이해할 수 있어야 한다.
- Client-server architecture : REST API 서버는 클라이언트에게 API를 제공하기만 한다. 클라이언트와 서버간의 역할분담이 명확하게 분리된다.
- Layered system(계층형 구조): Multi-layer로 구성될 수 있다. 중간에 존재하는 서버를 이용하여 Security관리, Encrypt, load balancing등을 수행할 수 있다. 확정성 및 보안 향상이 가능하다.
- Code on Demand : 서버에서 수행 스크립트를 받아 클라이언트 사이드 수행을 할 수 있다.

### 설계 원리
- `/` 슬래시는 계층 관계를 나타낸다. -> URI는 슬래시로 끝나지 않아야 한다.
- 리소스들의 집합 개념인 컬렉션은 복수s를 이용하고, 각각의 리소스 엘리먼트는 단수를 이용하는 것이 좋다.
- 언더 바 (_) 같은 문자를 쓰지 않는다.(-)하이픈을 쓴다.
- 소문자로 통일한다.(대소문자를 구별하기 때문에)
- 파일 확장자는 URI에 포함시키지 않는다. -> 확장자에 대한 설명까지 URI를 통해 알 수 있도록 풀어쓰는게 좀 더 좋다.

### Ajax와 REST
- Ajax 기반의 서비스는 콘텐츠가 바뀌어도 URL은 그대로여서 문제 발생
- `#!`
  - Ajax 통신을 통해 이동되는 페이지의 URI는 현재 URI의 #! 이후에 붙인다.
  - 구글에서 수집할 때 해당 #!이하의 URL을 판별해서 제대로 수집해주기 때문에 검색엔진에도 성공적으로 노출될 수 있다.
  - URI가 지저분해지는 단점
- `pushState`
  - javascript의 pushState를 통해 Ajax통신 후 변경된 컨텐츠의 URI를 제대로 바꿔줄 수 있다.
  - 최신 표준 브라우저에서만 지원..

## MIME type
- 참고: <https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types>
```
type/subtype
```

