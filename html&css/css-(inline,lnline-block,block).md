## inline / inline-block / block

### display / visibility
- display: 표시, 나타냄(어떻게 표시할지)
- visibility: 볼 수 있음(요소를 보일지 말지)

### inline element
- `<span>`, `<b>`, `<a>`, `<img>` 등
- 해당 요소 자기자신 만큼

### block element
- `<h1>`, `<p>`, `<div>`, `<ol>`, `<ul>`, `<table>` 등
- 해당 요소가 속한 줄 width 전체 100% 차지
- 다음 요소는 줄바꿈이 됨

### display: inline
- block 요소를 inline 요소처럼 만들어줌
- width, height 적용 불가
- margin,padding-top,bottom 적용 불가

### display: none
- 박스가 생성되지 않음 -> 공간을 차지하지도 않음

### display: block;
- inline 요소를 block 요소처럼 만들어줌

### display: inline-block
- 요소는 inline인데 내부는 block처럼 만들어줌
- 박스모양이 inline처럼 옆으로 늘어섬
