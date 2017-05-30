# FDS-15 : rwd실습 그리드 만들기
========


## 수업 전 테스트
- `javascript` : 사용자의 요구를 서버에 요청하는 역할.
- `DTD` : document type (문서유형정의) xml코드 
- lang속성
전역속성
lang속성과 language로 사용하지 않는다.
- 웹용 이미지포멧
`bmp` : 너무 용량큼
`jpeg` : 투명을 처리하지 못함.
`gif` : 좋았지만..
`png` : 최근에는 png-8은 투명처리 못함 인터넷익스6은 png를 처리하지 못함
`svg` : scaleable vector g (패스가 많아지면 용량이 커져)그래서 디자인이 더더욱 간단해지는것.
- 웹브라우저 해상도 : `96ppi`
css는 96ppi를 쓴다.
비트맵(이미지)는 72나 96은 사이즈 영향을 받지 않는다. 유일하게 폰트만 영향을 받는다.
`DPI` (Dot Per Inch) : 프린트 환경
`PPI` (Pixel Per Inch) : 스크린 환경
그러나 최근 구글에서 안드로이드 앱에서 dpi를 쓰며 그 경계는 없어짐.
gui - 마우스가 중심이 되는 시대
nui - 보이스, 터치 네추럴 인터페이스(인간 자체가 중심)
72ppi 사용은 예전. 제록스의 연구로 사용. 
- 웹 브라우저 기본 본문 글자 : `16px`
- <img> 요소 필수 속성 : `src` , `alt`
- id는 한번만 써야한다. 그렇지만 form 인풋 id는 꼭 해야한다.
- li 요소는 키보드 focus가 읽지 못한다. 
- inline 요소에 적용되지 않는것 : `text-align` / `width`
- mime type ??
- meta
<meta name="viewport" content="width=device-width, initial-scale=1">
이 코드는 비표준이지만 사실상 표준코드로 사용한다. 모든 브라우저가 지원한다.

<meta http-equiv="X-UA-Compatible" content="IE=Edge">
UA 유저 에이전트 IE6가 성공하면서 ms는 표준을 지키지 않는다. 그러다보니 다른 브라우저 들이 표준에 맞춰 개발하고, 오픈소스를 공유해서 성공하고 IE는 망해감. IE=Edge 

<meta property="og:type" content="product">
표준은 못할 수도 있지만 / 접근성은 강제성을 가진다.
이것을 적어줘야 카카오톡이나 그런곳에서 사진이랑 같이 뜬다.

<meta name="robots" content="noindex">
이것은 절대 쓰면 안된다. content="noindex" 이거는 개발중이니 오픈되지 않게 하는 코드. 그러나 정보는 오픈될 필요가 있다.

- ict 
- 예전에는 국제표준화를 따르지 않고, 한국표준화를 만든다. 

- `<a>` 태그안에 control이 있으면 블럭요소로 바꿀 수 없다.
- `<span>` 태그도 블럭요소가 아니다.
- `<ruby>` : 동아시아 문자들의 발음 표기 위해서 쓰는 태그
- `<progress>` : 상태 표시줄 다운로드모양
- `<dialog>` : 배경은 딤처리하고 가운데 뜨게 하는것 (팝업 레이어) 지금은 잘 사용되지 않는다.
- `<var>` : 수학식. 옛날에 존재하던 것. 지금은 실무에서 쓰지 않는다.

- `스프라이트 이미지` : 게임에서 왔다.
사용성 / 접근성 / 성능 중 성능을 위해서 (그러나 좌표값을 계산해야 되서 유지보수가 힘들다.)
- 청록색맹의 경우 색깔로 구분을 하는 디자인을 읽을 수 없다. 그래서 각 그래프의 아이콘을 달리줘야 구분할 수 가 있다.

- flex...
- `clearfix` 의 마이크로 클리어픽스 새로운 방법(오페라를 고려한것)
```css
.clearfix:before, .clearfix:after{
    content: "";
    display: table;
}
.clearfix:after{
    clear: both;
}
```
- 폰트 사이즈는 대문자 M의 세로 높이값.
- `em` : 인쇄에서 왔다. 대문자 M의 높이와 동일하다. 라는 말.(단점: 중첩이 되고, 중간에 바뀌면 안된다.)
- `rem` : em을 보완. 루트(html)의 기준으로 한다.
- em, px은 상대적

- css와 device의 pixel이 다르다.
심볼???어떻게 작업해야함??

- 부트스트렙 프론트 타이핑할때는 좋다. 와꾸만들때는 좋다. 그런데 디자이너는 이걸로 만들어주지 않기때문에 프론트엔드는 디자이너의 작업물을 프레임워크로 만들어야한다.

- 웹 브라우저 기본 설정 행간 비율 : line-hight , leading `1.2`
- `WCAG 2.0` 웹 접근성 UX, 소프트웨어,  정보통신 접근성
광과민성 발작 예방 - 운용(작동)
쉬운 내비게이션 - 운용
주 언어 명시 - 이해
대체 텍스트 - 인식
예측 가능성 - 이해
명료성 - 인식

- position : sticky
- 고대비 모드 : 저시력 장애자들이 사용. 
스프라이트 이미지는 성능성을 위해서 사용하지만 인터넷 익스플로러에서 접근성이 떨어진다.
이유 : 인터넷 익스플로러만 고대비 모드를 쓰면 스프라이트 이미지가 보이지 않는다.
- <img>
홈링크
대체 텍스트
404모드 : 클라이언트 오류
505모드 : 서버측 오류
- 갖다쓰는 문제
버튼이 아닌 a로 버튼을 쓰려면 aria기법을 써야한다.
그냥 div a로 묶어버린다면 스크린리더로 읽지도 못하고 키보드 포커스도 읽지 못한다.


---
## rwd 실습

- 고정값 그리드 / 유동적 그리드

### lang속성
ko-KR(랭귀지-위치)
```html
<!DOCTYPE html>
<html lang="ko-KR">
</html>
```

### 특수기호 표기(엠퍼샌드 기호)
- `&` : 특수 문자를 표현하기 위한 시작
- `;` : 특수 문자를 표현하고 끝마침
- `#` : ASCII 또는 Unicode 값으로 표현할때 사용  (10진수 변환 코드)
- `&lt;` : [<] less-than: ~ 보다 작다, 꺽쇠 열기 문자 기호
```html
<title>shopingmall &lt; yuyu.com</title>
```
```
shopingmall < yuyu.com
```
#### <<참고링크>>
- 특수기호 표기 : <http://nannarane.iptime.org/?p=460>


### position : sticky, split????
```css
position : sticky
```
```
$gutter-position : split
```

### linear-gradient 
```css
.show-grid::after{
    background: linear-gradient(180deg, transparent 20px, #0cf 20px);
    /* 기본 각도 180deg, 20px까지 transparent(투명), 20px부터 끝(21px)까지 파란색 */
    background-size: 1px 21px;
}
.show-grid::before{
    background: linear-gradient(90deg, transparent 10px, rgba(235, 107, 107, 0.29) 10px, rgba(235, 107, 107, 0.29) 80px, transparent 80px);
    background-size: 90px 1px;
}
```

### transform 속성
```css
transform: translateX(-50%);
    /* 화면의 중앙정렬, transform속성은 자기 기준으로 -50% 적용 */
```

### 컬럼 개수의 따른 is 값 구하는 공식
```
컬럼폭 * 컬럼개수 + 거터폭(합) * (컬럼개수 - 1)
VS math 단축키 : control + shift + y
VS 단어선택 단축키 : comm + D / D를 누른만큼 해당 단어 다중 선택
```
```css
.is-1 {width: 70px;}
.is-2 {width: 160px;}
```
```css
.is-2 {width: 70 * 2 + 20px * (2 - 1)px;}
```

## 과제
렉터 파일 
노멀라이즈 리셋 초기화 하는것을 분석해서
나만의 초기화 파일을 작업용파일 : 주석이 들어가야된다.
꼭필요한것만 두개의 파일 (min.css)

/* ! init.css @ */
주석 앞에 ! 넣으면 압축과정에서 안지워준다.

ul, li 기본스타일 초기화 하는것 그렇게 좋지 않아.


.is-1{width: 70px;}
.is-2{width: 160px;}

.is-2{width: (70 * 2) + (10 * 2) * 2}



## <<참고링크>>
- keycode : <http://keycode.info/>



