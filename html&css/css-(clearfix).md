## clearfix

* float취소
* http://ko.learnlayout.com/clearfix.html
* 부모에 특별한 너비나 속성을 추가하지 않으면 자식을 담아내지 못한다. 그리고 다음 요소에 영향을 준다.
* overflow: auto를 주면 담아낸다.
* clear: both => 빈요소를 사용했다는것, 내용과 표현의 분리로 권장 방법이 아님
* 부모요소에 ::before ::after 요소를 사용하여 요소를 블록요소로 만듦
    * `.부모::after { content: ‘’; display: table; clear: both; }`
* zoom: 1 => ie6,7 버전이 haslayout을 갖도록 해, 자식요소를 담기 위해 확장 됨