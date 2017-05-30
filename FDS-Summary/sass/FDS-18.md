FDS-18-sass Library
========



## <<참고링크>>
---
---
## susy 그리드 시스템 라이브러리
opacity 인터넷 익스플로러에서 i9부터 지원한다.

### 라이브러리
```sass
.box{
    +size(100px)
    +bg-color(#333, 0.45)
}
```


### 
// size(100 100) width, height
// 헥스 서드파티개발
// DRY dont repeat ???
// 알리아스
// 함수를 만드는 훈련
// 타인의 코드를 보는 훈련
// get함수(가져오는 함수): 꼭 return 값이 나와야 
// set함수
// 믹스인을 위에 써주고 css속성은 아래
// %center-box-block 이방법은 글이 몇줄이든 가운데 오게 한다.
// config파일 : 기본값 설정
// shade($color, $percent)
/// @example sass - margin 속성
/// 	@include margin(left auto right auto)


예전 라이브러리
bourbon


-----

### susy

mixin


base line : show / hide

image : show-grid-line ( 그리드라인만 그리겠다 




### 작업할때 susy그리드를 쓰고싶다면
작업하고자 하는 폴더 안에서($ npm install sassdoc -g 글로벌 설치가 끝났다면) 실행
```
$ npm i -D susy
```
[node-modules] - [sass]파일을 작업하는 sass폴더 안에 복사해서 이름을 [susy]라고 만들어주고 작업하면 된다.