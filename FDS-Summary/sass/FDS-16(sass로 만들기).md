# FDS-15 : rwd실습 sass로 만들기
========

#### <<참고링크>>
- sass 컬러 함수 : <http://sass-lang.com/documentation/Sass/Script/Functions.html>

포토샵
window
layer Comps
state (기본 / 로그인 / ... 등의 시각적인 것들)


네스팅박스
박스 중첩

isolate
격리시킨다.
플로트를 포지션처럼 쓴다.
음수마진 -100%;



## 포토샵에서 이미지 추출

### 구버전
슬라이스
다이싱

### 새버전(액션 만들기)
이미지 선택 후
액션파일만들기 버튼 - 이미지 레이어 위에서 오른쪽 - duplicate layer - set NEW - image trim - 액션메뉴에서 insertitemmenu - file - web for image
1,2,3배율 모두 자르기
이미지 위에서 오른쪽버튼 - duplicate layer
new- 
<http://retinize.it/>

cc 버전
plugin 체크 
제너레이트 - 이미지 에셋
logo 이름을 header/logo.png or logo@2x.png
이런식으로 이름 바꿔주면 자동으로 폴더생성되서 파일이 생김
뒤에 @2x를 넣어주면 2배율 이미지


### svg이미지 만들기
일러파일에서 이미지아트보드 (해당 아이콘 클릭하면 아트보드 만들어짐)만들고 save as 해서 range 1-8지정해 주고 내보내기 - 이름바꾸기