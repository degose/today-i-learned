* script 태그의 속성
    * </body>태그 직전 삽입 => 문서의 마지막에 스크립트 실행(스타일링이나 빨리 실행하고 싶다면 head 태그에 넣자.) 접속자들의 화면에 html구조와 css의 디자인을 먼저 적용하고 렌더링되면 문서 로딩의 체감 시간을 줄일 수 있음
    * type => 스크립트의 MIME타입 지정 => 프로그래밍 언어 말해주기. 
        * https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types
    * HTML5에서는 기본값이 text/javascript 생략 가능
    * defer => 스크립트 실행의 연기 -> 브라우저가 src속성을 만나게 되면 외부스크립트 파일에 집중하기 위해 html문서의 파싱을 잠시 미룸 -> 로딩 늦어짐. scr 외부 스크립트파일에 한정되므로 src도 함께 지정되야함
    * async => 스크립트의 비동기 실행 지정(defer와 비슷) 하지만 HTML 문서 파싱완료와 상관없이 스크립트 파일을 수신한 이후에 실행한다.