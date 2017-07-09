JavaScriptCookbook - 1 클라이언트-서버 통신 및 데이터
========

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
  - POST
  - PUT
  - DELETE
- 표현(Representations)
  - URI는 정보의 자원을 표현해야 한다.
  - 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현한다.
- '무엇을(HTTP URI로 정의된 리소스) 어떻게 한다(HTTP Method + Payload)'
### 특징
- Uniform(유니폼 인터페이스)
- Stateless(상태 없음)
- Casheable(캐시 가능)
- Self-descriptveness(자체 표현 구조)
- Client-server architecture
- Layered system(계층형 구조)

## MIME type
- 참고: <https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types>
```
type/subtype
```

