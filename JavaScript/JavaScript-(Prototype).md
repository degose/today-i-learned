## Prototype
- https://www.zerocho.com/category/Javascript/post/573c2acf91575c17008ad2fc 

### 프로토타입 객체
- 자바스크립트는 프로토타입 기반 객체지향 프로그래밍 언어
- 클래스 기반 객체지향 프로그래밍 언어는 객체 생성 이전에 `클래스`를 정의하고 이를 통해 객체(인스턴스)를 생성한다.
- 프로토타입 기반 객체지향 프로그래밍 언어는 클래스 없이도 객체를 생성할 수 있다.
- 객체 생성 방법
```javascript
// 객체 리터럴
var testObject = {};
// 선언과 동시에 인스턴스가 생성
var testPerson = {
  name: 'sese',
  gender: 'male'
};

// Object() 생성자 함수
// 빈 객체 생성
// 이후 프로퍼티와 메소드를 추가
var test = new Object();
test.name = 'sese';
test.gender = 'male';

// 생성자 함수
// 마치 객체를 생성하기 위한 템플릿(클래스)처럼 사용하여 구성이 동일한 객체를 여러개 생성할 수 있다. 앞문자를 대문자로
function Test(name, gender) {
  this.name = name;
  this.gender = gender;
}
// 인스턴스 생성
var person1 = new Test('sese','male');
var person2 = new Test('ko','female');
```
- 자바스크립트의 모든 객체는 자신의 부모 역할을 담당하는 객체와 연결되어 있다.
- 마치 객체 지향의 상속 개념과 같이 부모 객체의 프로퍼티 또는 메소드를 상속받아 사용할 수 있게 한다.
- 이러한 부모 객체를 Prototype 객체 라고 한다.
- 프로토타입 객체는 생성자 함수에 의해 생성된 각각의 객체에 공유 프로퍼티를 제공하기 위해 사용한다.

### `[[Prototype]]` 프로퍼티 vs Prototype 프로퍼티
- ECMAScript spec에는 자바스크립트의 모든 객체는 자신의 프로토타입을 가리키는 [[Prototype]]이라는 숨겨진 프로퍼티를 가진다.
- [[Prototype]] 프로퍼티는 자신의 프로토타입 객체를 가리키는 숨겨진 프로퍼티 이다.
- [[Prototype]] 프로퍼티는 `__proto__`로 구현되어 있어 같은 개념이다.
- Prototype 프로퍼티와 [[Prototype]]프로퍼티는 다르다.

