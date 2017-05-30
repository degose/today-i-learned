$ node-sass sass/ -o css/ --source-map true
$ node-sass --watch sass/ -o css/ --source-map true

node-sass sass/ -o css/ --output-style expanded --source-map true

노드사스를 불러올건데, sass폴더 하위에 있는건데, 아웃풋은 css/폴더에 있는거 할거야
아웃풋 스타일은 익스펜디드로 할거고, 소스맵은 개발자 도구에 오른쪽에 scss파일 어느 줄에 스타일이 있는지 알려주는 도구야

@for $i from 1 through 4{
.col-m-#{&i}{
width: 100px;
}
}

$list: mobile tablet desktop;
@each $device in $list{
.col-#{$device}{
width: 100px;
}
}
// list 변수 안에 값들을 한번씩 device에 담겠다.


$map:('h1': 20px, 'h2': 18px, 'h3': 16px,);
@each $heading, $size in $map{
.#{$heading}{
font-size: $size;
}
}

$map:('h1': 20px, 'h2': 18px, 'h3': 16px,);
@each $heading, $size in $map{
.#{$heading}{
font-size: $size;
}
}


```css
@import 'fonts';
@import 'normalize'; //브라우저 다른것 대응
@import 'reset';
@import 'base';
@import 'grid';
@import 'mixin';
@import 'header';
@import 'main';
@import 'footer';
```

여기서 선언해주는 순서가 중요하다.(폰트, 노멀라이즈)

<https://cdnjs.com/libraries/normalize>

여기 첫번째 파일 속 내용 복 붙


리셋도 여기 첫번째 파일 속 내용 복 붙
<https://cdnjs.com/libraries/meyer-reset>

```css
/* http://meyerweb.com/eric/tools/css/reset/ 
   v2.0 | 20110126
   License: none (public domain)
*/

html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
	margin: 0;
	padding: 0;
	border: 0;
	font-size: 100%;
	font: inherit;
	vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section {
	display: block;
}
body {
	line-height: 1;
}/* 라인하이트도 지워준다.(아마 1.5 주려고 하는듯?)*/
ol, ul {
	list-style: none;
}/* 여기 ol 태그는 지워준다. 왜냐면 순서가 필요한 리스트들이 있으니까 */
blockquote, q {
	quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
	content: '';
	content: none;
}
table {
	border-collapse: collapse;
	border-spacing: 0;
}
```
