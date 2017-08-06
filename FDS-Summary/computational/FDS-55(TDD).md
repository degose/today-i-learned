FDS-55-TDD
========

## TDD
- 테스트 주도 개발(Test Driven Development, TDD)

## Jasmine
### 단위테스트(unit test)
- 참고: <https://jasmine.github.io/pages/getting_started.html>
- 참고: <https://github.com/jasmine/jasmine#installation>
- 코드의 기능 단위를 테스트
- 스탠드얼론
- 카르마(현업에서 주로 씀) 자동화
```js
describe('hello world', ()=> { // 테스트 스윗: 테스트 유닛들의 모음 
  it('true is true', ()=> { // 테스트 유닛: 테스트 단위
    expect(true).toBe(true) // 매쳐: 검증자 
  })
})
```

### BDD(Behavior Driven Development)
- 유저 스토리 개념을 끌어들인 테스트 작성법
- Given, When, Then 


## 모듈패턴
### 모듈 생성 원칙
1. 단일 책임 원칙 - 모듈은 한 가지 역할만 한다.
2. 의존성 주입
