FDS-36-OOP,Store라이브러리,AJAX
========


## 객체 지향 프로그래밍(OOP)


### Store 라이브러리
- Vue.js에서 저장소 관리 객체
- 데이터 관리 CRUD
  - state(비공개)
- 사용자로 하여금 인터페이스
- init에서 option을 전달할 것 (예, 필수 데이터는 무엇이다. 이런식으로)

## 자바스크립트 패턴
- 참고: <https://scotch.io/bar-talk/4-javascript-design-patterns-you-should-know>
- 고프?? 각각의 디자인패턴 정의

### 모듈 패턴
- 참고: <http://yubylab.tistory.com/entry/%EB%94%94%EC%9E%90%EC%9D%B8-%ED%8C%A8%ED%84%B4-for-javascript-Module-Pattern>
### 싱글턴 패턴
- 참고: <https://www.zerocho.com/category/Javascript/post/57541bef7dfff917002c4e86>
- 하나의 생성자로 여러개의 객체를 만들 수 있지만, 하나의 생성자에 하나의 객체만을 만드는 패턴 -> 그리고 그 속성을 비공개로 만드는 것
- 객체 리터럴

### 팩토리 패턴
### 생성자 패턴
### 네임스페이스 패턴
### 샌드박스 패턴



## console.dir

## Object.assign()
- Object.assign(target, ...sources)
- sources 오브젝트로부터 target 오브젝트로 속성을 복사 -> target 오브젝트 반환
- 참고: <https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/assign>
```js
var obj = { a: 1 };
var copy = Object.assign({}, obj);
console.log(copy); // { a: 1 }
```
## Polyfill

## getter / setter


## 재귀함수 do while
## deep카피

## AJAX
## 디퍼 엔싱크
## 웹 2.0
- 참여, 공유, 개방 (이베이, 아마존)
## spa (singlepageapp)

## xmlHttp리퀘스트
## create / open / send
## 동기 / 비동기

## parseInt() 을 통한 숫자 변환

- 이 함수는 두번째 매개변수로 기수를 받는데, 보통 생략을 하지만 그러면 안된다. 파싱할 문자열이 0으로 시작하는 경우 8진수로 다뤄지는 경우가 있기 때문에, 예측 불가능한 경우가 생긴다.
```js
var month = "06",
 year = "09";

month = parseInt(month, 10);
year = parseInt(year, 10);
```
- 만약 기수를 생략 한다면, 09는 8진수로 취급되고 유효한 수가 아니기 때문에 0이 나올 것이다.
