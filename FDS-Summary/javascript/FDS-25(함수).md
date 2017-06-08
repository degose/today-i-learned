FDS-25-함순
========

========
### codeshcool 
========
```js
function mystery(){
    var secret = 6;
    function mystery2(multiplier){ //3
        multiplier *= 3;//9
        return secret * multiplier; // (스코프 체이닝) 6 * 9 = 54
    }
    return mystery2;
}

var hidden = mystery();
var result = hidden(3);

console.log('내가 생각한 값 : ',);
console.log('실제 결과 값: 54',result);
```

```js
function mystery(input){ //4 
    var secret = 5;
    function mystery2(multiplier){ //2
        multiplier *= input; // 2 * 4(스코프 체이닝)
        return secret * multiplier; // 5 * 8 = 40
    }
}

var hidden = mystery(4);

// 40
```

```js
function mystery(input) { // 3
  var secret = 4;
  input += 2; // 5
  function mystery2(multiplier) { // 6 -> 여기 무슨값이 들어오나? -> param(6) 가 들어오니까 6
    multiplier *= input; // 30
    return secret * multiplier; // 4 * 30 = 120
  } // 선언문은 일단 넘어감
  return mystery2; // hidden
}
function mystery3(param) { // pram을 함수로 받는다 6
  function mystery4(bonus) { // 2
    return param(6) + bonus; // (param = hidden = mystery2) -> 다시 mystery2에 6을 대입한 값 : 120 + 2
  } // 선언문은 그냥 넘어감
  return mystery4;
}
var hidden = mystery(3); // hidden은 mestery2  120
var jumble = mystery3(hidden); // mystery4 함수가 된다. -> 근데 왜 다시 mystery2가 되는거??
var result = jumble(2); // mystery4(bonus)에 2가 들어간다.
// 122
```
=========
### 함수만들기
=========

1) 
`warningMaker`라는 함수와 `monster`이라는 이름의 매개변수를 만든다. 이 함수 내에서는 특정 `monster`를 마주쳤을 때에 기반하여 특정한 `alert` 메시지를 보여주는 익명함수를 반환한다. 메시지 형식은 "Beware! There have been `<monster>` sightings in Seoul today!"로 한다.
참고: `warningMaker` 함수를 호출할 필요는 없음.
```js
function warningMaker(monster){
    return function(){ //익명함수
        alert("Beware! There have been '+ monster +' sightings in Seoul today!"); // '+ monster +' 부분
    }; // monster에 뭐가 들어가야하니까
}
```
2) 
서울에서 오크가 발견되었다는 보고가 있었다.
1번의 함수에 더하여,
- "Ork"를 매개변수 `monster`로 받아, `warningMaker` 함수에 인자로 전달하여 경고 메시지를 출력한다.
- 결과값은 `orkAlert`라는 새로운 변수에 저장한다.
- `orkAlert` 함수를 호출해 경고 메시지를 확인한다.
참고: `warningMaker` 함수를 변경하지 않는다.
```js
function warningMaker(monster){
    return function(){ //익명함수
        alert("Beware! There have been '+ monster +' sightings in Seoul today!");
    }; // monster에 뭐가 들어가야하니까
}
var orkAlert = warningMaker('Ork'); // 따옴표 넣었어야..
// alert("Beware! There have been '+ monster +' sightings in Seoul today!"); // 호출한다??

orkAlert(); // 호출

```
3)
`warningMaker` 함수를 변경하여 아래 조건을 경고 메시지 안에 반영해본다.
- 괴물(monster)의 수. 이건 무조건 첫 번째 매개변수여야 함.
- 괴물(monster)이 발견된 특정 위치. 이건 무조건 두 번째 매개변수여야 함.
즉, 특정한 숫자와 위치를 함수에 전달하고, 해당 값들을 `warningMaker` 함수에 전달되는 `alert` 메시지에 포함되도록 한다.
`warningMaker` 함수를 업데이트하여, 메시지 형식은 아래와 같이 한다. 매개변수를 사용해 중괄호({}) 부분을 수정한다.
"Beware! There have been <monster> sightings in Seoul today!
<number> have been spotted at the <location>!" 
참고: 공백에 주의하라. `warningMaker` 함수를 수정할 필요는 없다.
```js
function warningMaker(monster){
    return function(number, location){ 
        alert("Beware! There have been" + monster + "sightings in Seoul today!" + number + "have been spotted at the" + location + "!" );
    };
}
```
4)
아래와 같은 경고 생성기를 몇 개 더 만들었고 갑자기 발생하는 위험에 대비하기로 했다.
    Mayday, mayday!
    I've got `6` green hulks near "Gwanghwa-mun"!
    And `1` snow yeti across "Nam San"!
    Over and out!
위와 같이 이미 만들어진 경고 메시지를 검토하고, 이 상황에 맞는 적절한 함수를 호출해라. 적절한 매개변수를 넣는 것 또한 잊지 마라. 딱 코드 두 줄이면 된다.
```js
function warningMaker(monster) {
  return function(number, location) {
    alert("Beware! There have been " + monster +
          " sightings in Seoul today!\n" +
          number + " have been spotted at the " +
          location + "!");
  };
}
var greenHulkAlert = warningMaker("green hulk");
var xManAlert     = warningMaker("x man");
var orkAlert       = warningMaker("ork");
var flashBlizzardAlert = warningMaker("flash blizzard");
var snowYetiAlert      = warningMaker("snow yeti");
// call the two functions here
greenHulkAlert(6,"Gwanghwa-mun");
snowYetiAlert(1,"Nam San");
```
5)
위와 같은 함수에서는, 어떤 괴물은 여러 번 경고를 하지만 다른 것들은 그렇지 못하다.
`warningMaker` 함수를 수정해서 특정 경고가 발현된 횟수를 내부적으로 세는 방향으로 수정해 본다.
이를 위해서는, `count` 변수를 설정하고 함수 문맥(context) 내에서 이를 적절하게 증가시키는 방법을 알아내야 한다.
마지막으로 `count`를 `alert` 메시지에 넣는다. 메시지 형식은 아래와 같아야 한다.
Beware! There have been <monster> sightings in Seoul today!
<number> have been spotted at the <location>!
This is alert #<count> today for <monster> danger.
```js
function warningMaker(monster) {
  // create a count
  // var count += number
  var count = 0; // 초기화
  return function(number, location) {
    // keep track of warnings
    count++; // 이렇게 증가시켜줘야
    alert("Beware! There have been " + monster +
          " sightings in Seoul today!\n" +
          number + " have been spotted at the " +
          location + "!\n" +
          // finish the warning message here
          "This is alert" + count + "today for" + monster + "danger."
    );
  };
}
```
6)
각각의 `location`을 저장해서, 새로운 경고 메시지가 뜰 때마다 `monster`에 대한 위험지역이 리스트 형태로 나오게 만들어라.
`warningMaker` 함수 내부에는
- 각각의 `location`을 `zone`이라는 배열 안에 저장한다.
- `zone`을 `list` 문자열 안에 추가한다.
- `alert` 메시지 안에 위험지역에 대한 `list`가 뜰 수 있도록 한다. 포맷은 아래와 같다.
Beware! There have been <monster> sightings in Seoul today!
<number> have been spotted at the <location>!
This is alert #<count> today for <monster> danger.
Current danger zones are:
`<zone1>`
`<zone2>`
`<zone3>` - > 이것을 스트링으로 만들어라
```js
function warningMaker(monster) {
  var count = 0;
  var zones = [];
  return function(number, location) {
    count++;
    var list = "";
    // add each location to the zones array
    zones.push(location);
    // add each zone to the list string
    // list + "zone1";
    for(var i=0, l=zones.length; i<l; i++)
        list += zones[i] + '\n';
    }
    // zones.join('\n');
    // ['aa','bb','cc','dd'].join(''); 빈 문자열을 넣으면 합쳐진다.
    // -> 'aabbccdd' 
    // ['aa','bb','cc','dd'].join('-'); -이 사이에 더해진다.
    // -> 'aa-bb-cc-dd' 
    alert("Beware! There have been " + monster +
          " sightings in Seoul today!\n" +
          number + " have been spotted at the " +
          location + "!\n" +
          "This is alert #" + count +
          " today for " + monster + " danger.\n" +
          // finish the warning message here
          "Current danger zones are: \n" + 
          list
    );
  };
}
```
7)
위험지역을 피하는 게 아니라, 스릴을 즐기고 싶은 사람이 있을 수도(!) 있다. 실제로 괴물이 많은 지역을 한번 구경하기를 원하는 사람도 있을 것이다.
위험지역 목록을 가지고 있으니, 한번 각 위치 옆에 `number`을 추가해보자.
- `zones` 배열을 사용해서, `monster`에 대한 `location`과 `number`가 모두 포함된 하위 배열을 `push`한다.
- `for`문 안에서 `zones` 배열 값에 접근하여 이를 `list` 문자열에 더하는 방법을 찾아본다.
- 최종 `alert`는 아래와 같은 형태로 나와야 한다.
Beware! There have been <monster> sightings in Seoul today!
<number> have been spotted at the <location>!
This is alert #<count> today for <monster> danger.
Current danger zones are:
<zone1> (<number1>)
<zone2> (<number2>)
<zone3> (<number3>)

참고: `alert` 메시지를 바꿀 필요가 없다. `zones` 배열을 바꾸고 `for`문을 수정해서 `list` 문자열에 제대로 된 값이 들어갈 수 있도록 만들면 된다.
```js
function warningMaker(obstacle) {
  var count = 0;
  var zones = [];
  return function(number, location) {
    count++;
    var list = "";
    // push an array with location and number
    list.push([location,number]);// []묶어줘야
    for (var i = 0; i < zones.length; i++) {
      // replace location and number with appropriate code
      list += zone[i][1] + " (" + [i][0] + ")" + "\n";
    }
    alert("Beware! There have been " + obstacle +
          " sightings in the Cove today!\n" +
          number + " have been spotted at the " +
          location + "!\n" +
          "This is alert #" + count +
          " today for " + obstacle + " danger.\n" +
          "Current danger zones are:\n" +
          list);
  };
}
```

=======
### 6/7 함수 연습 (codeschool 예제)
=======

1.

한 개발자가 아래와 같이 `forestFright`라는 함수 선언을 만들어 두었지만, 메모리 상에 보관하지 않기로 결정했다. 이 함수를 익명 함수 표현식으로 바꾸고, `runaway`라는 변수에 할당해라.

```js
function forestFright() {
  var toAlert = "";
  for (var i = 0; i < 5; i++) {
    toAlert = toAlert + "Lions, Tigers, and Bears, Oh My!!\n";
  }
  alert(toAlert);
}
```


2. 

최병광 조교님은 수강생들의 행복지수를 조사하고자, 아래와 같은 특별한 수식을 만들었다. 이 식은 시험 점수, 출석률, 수업 만족도를 기반으로 만들었다.
```js
var happinessGenerated = function(testScore, attendanceRate, satisfactionLevel) {
  var ability = testScore * attendanceRate;
  var feeling = satisfactionLevel * satisfactionLevel * satisfactionLevel;
  var totalHappiness = feeling + ability;
  return totalHappiness;
};
```
- `happinessGenerated` 공식을 분석해라.
- `test`, `attendance`, `satisfaction` 변수에 적절한 값을 넣어, 수강생 성취도가 100점 초과, 400점 미만이 되도록 만들어라.
- `happinessGenerated` 함수를 호출하고 인자에 변수를 넣어라.
- 그 값을 새로운 변수인 `happiness`에 저장한다.

```js
var test = /*//fill this in//*/;
var attendance = /*//fill this in//*/;
var satisfaction = /*//fill this in//*/;

var happinessGenerated = function(testScore, attendanceRate, satisfactionLevel) {
  var ability = testScore * attendanceRate;
  var feeling = satisfactionLevel * satisfactionLevel * satisfactionLevel;
  var totalHappiness = feeling + ability;
  return totalHappiness;
```

3.

`alert`를 통하여, 위 `happinessGenerated` 함수를 실행하는 것이 아니라 함수 내용을 보여주려면 어떻게 해야 할까?

4. 

조교님은 행복지수에 따라 수강생들에게 알림 메시지가 가도록 코드를 짜려고 한다. 
- `happinessMessage` 함수 표현식에는 조건문(if ~ else 등)을 넣어 `happiness` 정수값을 체크하려고 한다. `happiness`의 범위에 따라서, `confirm` 함수를 호출하는 것을 반환한다. 200보다 적으면 아래와 같이 출력되도록 반환한다.
```
Happiness Level: LOW
계속 하실 수 있죠?
```
`happiness`가 200에서 300 사이(fear >= 200 && fear <= 300)라면,
```
Happiness Leve: MEDIUM
끝까지 가보자구요. 가능하죠?
```
를 반환한다.

```js
var fear = fearGenerated(numPeeps, rainInInches, numSharks);

var fearMessage = function() {
  // Insert conditional statements here

};

function confirmRide(confirmToGo) {
  return confirmToGo();
}

// Call confirmRide with the fearMessage function
var startRide = confirmRide(fearMessage);

```

5. 

1)
패스트캠퍼스 문 앞에, 인사말과 함께 방문자의 이름을 보여주는 전광판을 달아둘 예정이다. 문제는 데이터에 성과 이름이 분리된 하위 배열로 이뤄져 있다는 점이다. `passenger` 배열에서 각 방문자의 성과 이름을 합쳐 문자열로 변환하려 한다.

- `modifiedNames` 변수를 만들고 새로운 데이터를 저장한다.
- `passengers.map()`를 `modifiedNames` 변수에 지정한다. 이렇게 하면, 배열의 모든 엘리먼트에 사용할 수 있는 함수를 전달할 수 있다.
- `map()`에 익명함수를 전달한다.
- 익명함수는 `arrayCell`을 매개변수로 사용하며, 이 매개변수를 사용하여 승객의 성과 이름(문자열)을 반환한다. 즉, ["홍", "지수"] 배열을 전달한다면, 함수는 "홍지수"라고 문자열로 반환해야 한다.

```js
var passengers = [ ["홍", "지수"],
                   ["최", "병광"],
                   ["지", "훈"],
                   ["김", "데레사"] ];
                   
```

2) 드디어 방문자가 신관에 도착했다. 1)번에서 만든 `modifiedNames` 배열을 이용하고, 새로운 익명함수에 `map`을 하여 넣어둔다.

각각의 방문자가 왔을 때 아래 메시지를 `alert`한다.

`반갑습니다, <name>님!`

참고: 값을 반환하거나 새로운 변수를 만들 필요는 없다. 물론 `map`이 반환한 값을 사용하면 되지만, 이건 그냥 연습일 뿐이니까!
```js
var passengers = [ ["홍지수"],
                   ["최병광"],
                   ["지훈"],
                   ["김데레사"] ];
```

6. 

1) 
한 여행사에서 세 종류의 여행상품을 만들었다. 고객에게 어떤 숫자를 선택할 것인지 물어본다. 이 숫자는 `userChoice`에 저장된 후에 `adventureSelector` 함수로 전달된다.

함수 내부에서 고객이 선택한 숫자를 기반으로 익명함수를 반환해야 한다. 세 가지 익명함수는 아래와 같은 경고 메시지가 뜬다.

고객이 1을 선택했다면:
"제주도 여행을 선택하셨군요!"

고객이 2를 선택했다면:
"울릉도가 울렁울렁!"

고객이 3을 선택했다면:
"안!면!도!"

고객이 선택한 것이 이미 1, 2, 3으로 저장됐고 `userChoice`의 매개변수로 전달되었다고 가정해보자. 모든 메시지가 변수에 저장되지 않고 익명함수로 반환되는지 확인해보라. 
```js
function adventureSelector(userChoice) {
  // return anonymous functions inside conditional blocks
}
```
2)
adventureSelector를 호출하고 3을 인수로 전달하는 코드를 작성해라. 즉시 실행 함수가 호출되어야 한다.



======
======

1)
수강생이 강의장에 오면, flowerList 배열에서 인덱스에 해당하는 사람에게 아래와 같이 주려고 한다.

- 원본
```js
function assignFlower(student, flowerList) {
  var classroomAssignment;
  for (var i = 0; i < flowerList.length; i++) {
    if (student == flowerList[i]) {
      classroomAssignment = function() {
        alert("안녕하세요, " + student + "님!\n" +
        "강의장에 오시면 " +
        (i + 1) + " 을/를 선물로 드릴게요.");
      };
    }
  }
  return classroomAssignment;
}
```

- 수정
```js
function assignFlower(student, flowerList) {
  var for (var i = 0; i < flowerList.length; i++) {
    if (student == flowerList[i]) {
      return function() {
        alert("안녕하세요, " + student + "님!\n" +
        "강의장에 오시면 " +
        flowerList[i] + " 을/를 선물로 드릴게요.");
      };
    }
  }
}
```



======
### 별 찍기
======
*
***
*****
***
*
```js
for(var i=0; i<; i++)
```


#### 디버거 콘솔
- Sources -> snippets추가 해서 -> 빈 문서에 코드 붙여넣고 -> 북마크 한 뒤 -> 로딩