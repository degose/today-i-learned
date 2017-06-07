FDS-24-IIFE / 클로저 / 모듈
========

## 즉시 실행 함수(IIFE)
- 함수식을 사용하는데 변수에 할당하지 않고 자기 스스로 실행
- `var fn = function(){}();` -> 함수값(); 실행
- 예시
- `toFixed()`: 소수점의 자리수를 제한하여 String으로 반환함.
- 보통 앞에 `to`가 붙으면 string으로 반환
```js
m = 9.2352
m.toFixed(2) // "9.23" -> 문자열로 바꿔주는데 소수점 2자리까지 바꿔줌
+m.toFixed(2) // 9.23 -> 숫자열로 바꿔줌
```
- 이름 호출 없이 즉시 실행되는 JavaScript 프로그래밍 언어의 관용어구 : 이디엄(idom)
```js
(function(){})();
(function(){}());
// 객체 값을 변수에 참조한 예
var memorial_card = {};
// IIFE 패턴을 사용하여 실행된 결과 값 객체를 반환 받은 변수 예
var another_memorial_card = (function(){
    return {};
}());
```

## 모듈(Module) 패턴
- Front-End 환경에서는 js파일이 독립적이지 않아서 하나하나 html로 불러와야한다. -> 각 js파일에서 모두 전역에 노출된 상태이기에 같은 이름의 변수, 함수는 충돌이 발생하는 문제가 발생한다.
- > `모듈패턴`을 이용하면 전역과 구분되는 영역을 만들어 그 내부 변수,함수가 외부에 노출되지 않아서 충돌이 일어나지 않게 방지할 수 있다.
- > JavaScript는 모듈이라는 것을 지원하지 않지만, `IIFE 패턴`을 이용하여 모듈처럼 사용할 수 있다. 
- > IIFE패턴을 사용하여 전역과 구분되는 영역(모듈)을 만들었지만, 외부에서 접근이 불가능한 `은폐된 (private)공간`이 형성된다. 그렇게되면 내부 함수를 쓸 수없어 재사용 할 수 없게 된다.
- > 그러므로 `Namespace패턴`을 이용하여 외부에 하나의 변수를 선언한 후 그 속성으로 변수,함수를 할당하여 접근할 수 있다.(왜냐면 변수 안에 속성으로 들어있다면 -> 변수.속성으로 접근이 가능하니까.)

### 노출(명시적 공개)패턴
- 함수가 반환(return)하는 값(객체,배열,함수,불리언,숫자,문자,null)

### Namespace패턴
- 전역에서 접근 가능한 객체(Namespace)를 하나 정의한 후,
- > 각 모듈의 코드 로직을 Namespace객체의 속성으로 할당한다.

- IIFE 패턴을 활용
```js
(function(
    // 지역변수가 된다.
    // 충돌이 나지 않는다.
    // 은폐된(private)공간이 형성
    var module = function () {
        console.log('A file. Function.')
    };
    // 외부에 접근 가능하도록 공개
    return module;
}());
```

- 네임스페이스 패턴을 활용
```js
(function(global, $){ // (매개변수)global - window / $ - FDS 를 가리킨다.
    var module = function () {
        console.log('A file. Function.')
    };

    //전역에 명시적으로 공개하는 방법
    //네임스페이스 객체를 사용하여 속성으로 모듈 로직을 할당(공개)
    // 전역에 fds변수가 null,undefined 이거나,
    // fds 변수에 할당되어 있는 값이 객체(object)가 아닌 경우
    // 조건은 참이다.
    if(!global.fds || !isObject(global.fds)){
        // 전역 fds 변수에 빈 객체로 초기화 하라.
        global.fds= {};
    }
    // fds 변수는 확실하게 객체이다.
    // 이렇게 공개할 수 있다.
    // global.fds.sayWhatTypeOfFunction = module; // sayWhatTypeOfFunction이라는 메서드를 만들어줌
    $.sayWhatTypeOfFunction = module; 

// }(window));
}(window, (window.fds = window.fds || {}))); // - 인자
``` 

## 클로저(Closures)
- 한번 실행된 지역변수는 사라져야한다. 그런데 클로저현상(?)으로 인해 밖에서 사라진 지역변수를 실행할 수 있다.
- 히어로물에서 영웅이 죽는다 -> 그런데 다음편에 죽었던 영웅이 다시 등장해 -> 그 이유는 영웅은 일급객체 즉 전지전능한 객체이기 때문에 -> 단, 참조하고 있어야한다. -> 이러한 현상을 클로저라고 한다.
- 예시 (1씩 증가하는 함수)
```js
// 함수를 변수에 담아줬다.
var countMaker = function () {
    var count = 0;
    // 내부 함수
    function increaseCount() {
        // var count = 0;
        return ++count;
    }
    // 내부 함수를 외부로 내보낸다.
    // increaseCont(); 이거랑 뭐가다르다고??? -> 함수 자체를 실행 시키는 것 -> 값이 나오고 값은 -> 복사
    return increaseCount; // 이거를 내보내줘서 밖에서도 안에서 소멸된 함수를 실행해 주는거? 아니면 이런거 없어도 밖에서 소멸된 함수를 실행해준다? -> 이렇게 내보내줘야하는것! 이게 없다면 다 사라져버림 -> 함수를 참조
};
// 소멸된 지역코드가 실행된다.
increaseCount(); // 1 실행된다.
increaseCount(); // 2 실행된다.
increaseCount(); // 3 실행된다.
increaseCount(); // 4 실행된다.

// 응용 (1씩 작아지는 함수)
var countDownMaker = function (n) {
    var count = n || 10;
    // 내부 함수
    return function (step) {
        return count - (step || 1);
    }
};

var countDown10 = countDownMaker(); // return function() {}
var countDown20 = countDownMaker(20); // 19,18,17,16...
var countDown45 = countDownMaker(45); // 44,43,42,41...
var countDown100 = countDownMaker(100); // 99,98,97,96...

// 응용
var countUpMaker = function (n){
    // var count = n || 10;
    // return function () {
    //     return ++count;
    // }
    n = n || 10;
    return function (step) {
        return n + (step || 1);
    }
    // 왜 이렇게 써줬냐면 지금 변수에서 n이 없으니 상위 매개변수에서 찾고 거기없으면 더 큰 상위 매개변수에서 찾게되니까
};

var countUp10 = countUpMaker();
```

## 클로저 활용 1 
- 클로저는 함수 뿐만 아니라, 모든 데이터 유형을 반환할 수 있다.
- > 객체를 반환하는 래퍼 함수를 사용하여 클로저를 활용할 수 있다.
- > 외부로 유출된 데이터가 함수 내부의 영역의 기억을 가지고 있다면
```js
function makeCountManager(init_count) {
    // 관리할 카운트 값을 초기화
    init_count = init_count || 0;
    
    // 함수내부의 기억을 가지고 있는 객체(데이터)들을 외부로 유출
    return {
        // 카운트 증가 메서드
        increase: function(step){
            init_count += (step || 1);
            return init_count;
        },
        // 카운트 감소 메서드
        decrease: function(step){
            init_count -= (step || 1);
            return init_count;
        },
        // 카운트 초기화 메서드
        reset: function (value) {
            init_count = value || 0;
        },
        // 현재 카운트 값을 반환하는 메서드
        getCount: function(){
            return init_count;
        }
    };
}
```


## 클로저 활용 2 (Model.js 파일)
- (이 부분 개념정리 후에 다시 보기)
- 데이터를 관리하는 객체를 생성하는 모듈을 가진 파일
```js

// 실행
// Model();
// var book_collection = Model();
// 배열은 변수에 할당
// 배열은 다수의 아이템(객체)을 가진다.
// 초기 값 설정: 배열은 초기 데이터(아이템)을 소유할 수 있다.
// 변경 가능: 추후에 아이템을 추가/제거/수정 할 수 있따. -> 메서드를 만들 수 있다.


console.log('classUsingArray');

// Model 함수를 정의
var Model = function(g,$){ // 왜 매게변수로 global , $(FDS)를 받나? -> window에 메서드를 가져다 쓸 때, 명시적으로 적어주지 않으면 안에서 쓰는 window를 찾기위해 바깥(전역)에 나갔다와야하는데 그 비용을 절감하기 위해서
  // FDS 모듈이 존재하지 않을 경우 -> 오류 발생
  if ( !FDS ) { throw 'Model.js는 FDS 모듈에 의존하는 개발 파일입니다.' }

  return function(data) {
    // 관리할 초기 데이터 설정
    data = FDS.isArray(data) ? data : [];

    var _modelManager = {
      // 객체의 멤버 정의
      // 등록(추가)
      add: function(item, direction) {
        validateError(item, 'undefined', '인자를 전달해주세요');
        direction = direction === 'before' ? 'unshift' : 'push';
        // data.push(item);
        data[direction](item); //이거 왜 이렇게 쓴다고?
      },
      // 변경(수정)
      // 제거
      remove: function(item, direction) {
        validateError(item, 'undefined', '인자를 전달해주세요');
        direction = direction === 'before' ? 'shift' : 'pop';
        // data.push(item);
        data[direction](item);
      },
      // 현재 관리 데이터 가져오기
      getData: function() {
        return data;
      },
      getDataCount: function() {
        return data.length;
      }
    };

    return _modelManager;
  }

}(window, window.FDS);



//실행
var classmate = Model(classUsingArray); // undefined
classmate.add({
    name: '후이즈몰',
    age: 10,
    majer: '전자상거래',
    school: {
        name: '가야대',
        grade: 2
    }
}, 'before');
```

