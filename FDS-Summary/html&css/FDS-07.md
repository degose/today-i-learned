FDS-07
========
---

 ## <<참고링크>>

 - fontello <http://fontello.com/>
 - <https://code.jquery.com/>

---

## <<새로 배운 속성>>

- box-shadow
```css
box-shadow: 5px 5px 5px 0 rgba(0,0,0,0.5);/* x,y,블러,? */
```

- text-overflow: ellipsis;

- placeholder - input 안에 들어가는 텍스트
```html
<input type="search" id="search-keyword" required placeholder="검색어를 입력하세요.">
```

- 제이쿼리 스크립트
```html
<script>
    $(function(){
        $(".tab").click(function(e){
            e.preventDefault();
            $(this).parent().parent().addClass("board-active")
            .siblings().removeClass("board-active");
        });
    });
</script>
```
```css
.pds-list a{
    display: inline-block;
    width: calc(100% - 90px);
    white-space: nowrap;
    overflow: hidden;/* 독립된 상자가 되면서 안에 컨텐츠가 인라인컨텐츠가 되어서 틈이 생김 */
    text-overflow: ellipsis;
}
```
---
## <<몰랐던 단어>>

- svg
>스케일러블 벡터 그래픽스(Scalable Vector Graphics, SVG)2차원 벡터 그래픽을 표현하기 위한 XML 기반의 파일 형식. 그 작동은 XML 텍스트 파일들로 정의 되어 검색화·목록화·스크립트화가 가능하며 필요하다면 압축도 가능하다.


---

## <<webcafe 실습>>

### 컬럼2 - 검색 / 탭메뉴 / 
---
#### 검색

- 내가 짠 markup
```html
<div class="group group2">
    <div class="search">
        <h2 class="search-heading">자료검색</h2>
        <form action="" class="search-form">
            <fieldset>
                <legend>자료검색 폼</legend>
                <div>
                    <label for="user-search">자료검색</label>
                    <input type="" id="user-search" required>
                </div>
                    <button type="" class="btn-search">검색</button>
            </fieldset>
        </form>
    </div>
</div>
```

- 논리적구조설계

>1. 자료검색
>2. 검색어 입력상자
>3. 검색버튼


> form action="javascript:alert('검색이 완료되었습니다.')"
action값 없으면 유효성검사시 오류 나온다. "안에서는 '홀따옴표'"

** required
** 논리속성



- 다시 짠 markup
```html
<div class="group group2">
    <div class="search">
        <h2 class="a11y-hidden">검색</h2>
        <form action="javascript:alert('검색이 완료되었습니다.')" class="search-form">
            <fieldset>
                <legend>검색 폼</legend>
                    <label for="search-keyword">자료검색</label>
                    <input type="search" id="search-keyword" required placeholder="검색어를 입력하세요.">
                    <button class="btn-search">검색</button>
            </fieldset>
        </form>
    </div>
</div>
```
- 내가 짠 css
```css
/* 검색 */
.group2{
    background: tomato;
    width: 380px;
}
/*.search{
    background: silver;
}*/
.search-form{
    background: linear-gradient(to bottom, #aaa, #fff);
    border-top: 1px solid #333;
    border-left: 1px solid #333;
    border-right: 1px solid #333;
    height: 50px;
    border-radius: 20px 20px 0 0;
    padding: 20px 20px 0 20px;
}
.search-form fieldset{
    /*background: silver;*/
    margin: 0;
    padding: 0;
    border-style: none;
    padding: 0;
}
.search-form label{
    margin: 0 5px 0 3px;
}
.search-form label::before{
    content: "z";
    font-family: 'webcafeIcon';
    position: relative;
    top: 2px;
}
.search-form input{
    margin: 0;
    padding: 0 0 0 3px;
    border: 1px solid #aaa;
    height: 20px;
    width: 200px;
    border-radius: 1px;
}
.btn-search{
    background: linear-gradient(to bottom, #888, #333);
    color: #fff;
    width: 42px;
    height: 22px;
    border: 1px solid #aaa;
    border-radius: 2px;
    margin: 0 0 0 10px;
    padding: 0;
}
```

현업에서 버튼에 a태그를 많이 쓰는이유 : 키보드 포커스 가능하고 올렸을때 손가락 모양으로 당연히 바뀌니까.

문제 : 읽어줄때 버튼이 아니라 링크로 읽어준다 그럴때 ??으로 링크가 아니라 버튼이야 말해주면 된다.

- 다시 짠 css
```css
/* 검색 */
.group2{
    /*background: tomato;*/
    width: 380px;
}
.search{
    border: 1px solid #aaa;
    border-bottom-color: #fff;
    border-radius: 20px 20px 0 0;
    padding: 15px 25px 10px 25px;
    background: #ccc linear-gradient(to bottom, #ccc 0%, #eee 60%, #fff 100%);
}
.search-form fieldset{
    margin: 0;
    padding: 0;
    border: 0;
}
.search-form label{
    margin-right: 5px; 
}
.search-form label::before{
    content: "z";
    font-family: 'webcafeIcon';
    font-size: 1.6rem;
    position: relative;
    top: 3px;
}
.search-form input{
    box-sizing: border-box;
    width: 200px;
    height: 22px;
    border: 1px solid #aaa;
    border-radius: 3px;
    padding: 1px 1px 1px 5px;
    margin-right: 4px;
}
.btn-search{
    border: 1px solid #aaa;
    background: #333 linear-gradient(to bottom, #999, #333);
    color: #fff;
    padding: 1px 10px 1px 10px;
    font-size: 1.3rem;
    border-radius: 3px;
}
```

---
#### 탭메뉴

- 내가 짠 markup
```html
<div class="tab-menu">
    <div class="notice">
        <a href="#" class="notice">공지사항</a>
        <ul class="list">
            <li a href="#">HTML 모든 것을 알려주마 샘플 활용법</li>
            <li a href="#">W3C 사이트 리뉴얼 소식 및 공지사항</li>
            <li a href="#">KWCAG2.0 소식</li>
            <li a href="#">서버 점검으로 인한 사이트 이용안내 입니다.</li>
            <li a href="#">여러분들이 생각하는 웹 접근성에 대해 이야기를 나누어 봅시다.</li>
        </ul>
        <ul class="date">
            <li>2017.05.10</li>
            <li>2017.05.10</li>
            <li>2017.05.10</li>
            <li>2017.05.10</li>
            <li>2017.05.10</li>
        </ul>
    </div>
    <div class="pds">
        <a href="#" class="pds">자료실</a>
        <ul class="list">
            <li a href="#">디자인 사이트 링크 모음</li>
            <li a href="#">웹 접근성 관련 자료 모음</li>
            <li a href="#">예제 샘플 응용해 보기</li>
            <li a href="#">웹 접근성 향상을 위한 국가표준 기술 가이드 라인</li>
            <li a href="#">로얄티 프리 이미지 자료</li>
        </ul>
        <ul class="date">
            <li>2017.05.10</li>
            <li>2017.05.10</li>
            <li>2017.05.10</li>
            <li>2017.05.10</li>
            <li>2017.05.10</li>
        </ul>
    </div>
    <a href="#" class="btn-more">더보기</a>
</div>
```
- 논리적 구조설계

>1. 공지사항
>2. 목록
>3. 더보기
>4. 자료실
>5. 목록
>6. 더보기

- 다시 짠 markup
```html
<div class="board">
    <div class="notice board-active">
        <h2 class="notice-heading">
            <a href="#" class="tab">공지사항</a>
        </h2>
        <ul class="notice-list">
            <li>
                <a href="#" class="board-subject">HTML 모든 것을 알려주마 샘플 활용법</a>
                <time class="board-date" datetime="2017-05-10">2017.05.10</time>
            </li>
            <li>
                <a href="#" class="board-subject">W3C 사이트 리뉴얼 소식 및 공지사항</a>
                <time class="board-date" datetime="2017-05-10">2017.05.10</time>
            </li>
            <li>
                <a href="#" class="board-subject">KWCAG2.0 소식</a>
                <time class="board-date" datetime="2017-05-10">2017.05.10</time>
            </li>
            <li>
                <a href="#" class="board-subject">서버 점검으로 인한 사이트 이용안내 입니다.</a>
                <time class="board-date" datetime="2017-05-10">2017.05.10</time>
            </li>
            <li>
                <a href="#" class="board-subject">여러분들이 생각하는 웹 접근성에 대해 이야기를 나누어 봅시다.</a>
                <time class="board-date" datetime="2017-05-10">2017.05.10</time>
            </li>
        </ul>
        <a href="#" class="notice-more" title:"공지사항" target="_blank">더보기</a>
    </div>
    <div class="pds">
        <h2 class="pds-heading">
            <a href="#" class="tab">자료실</a>
        </h2>
        <ul class="pds-list">
            <li>
                <a href="#" class="board-subject">디자인 사이트 링크 모음</a>
                <time class="board-date" datetime="2017-05-10">2017.05.10</time>
            </li>
            <li>
                <a href="#" class="board-subject">웹 접근성 관련 자료 모음</a>
                <time class="board-date" datetime="2017-05-10">2017.05.10</time>
            </li>
            <li>
                <a href="#" class="board-subject">예제 샘플 응용해 보기</a>
                <time class="board-date" datetime="2017-05-10">2017.05.10</time>
            </li>
            <li>
                <a href="#" class="board-subject">웹 접근성 향상을 위한 국가표준 기술 가이드 라인</a>
                <time class="board-date" datetime="2017-05-10">2017.05.10</time>
            </li>
            <li>
                <a href="#" class="board-subject">로얄티 프리 이미지 자료</a>
                <time class="board-date" datetime="2017-05-10">2017.05.10</time>
            </li>
        </ul>
        <a href="#" class="pds-more" title:"공지사항" target="_blank">더보기</a>
    </div>
</div>
```
li*5>a.board-subject+time.board-date[datetime="2017-05-10"]{2017.05.10}

- 내가 짠 css
```css
/* 게시판 */
.board{
    background: pink;
    position: relative;
}
.notice{
    background: yellow;
    position: relative;
}
/*.pds{
    position: relative;
}*/
.notice-heading, .pds-heading{
    font-size: 1.5rem;
    margin: 0 0 10px 0;  
}
/*.pds-heading{
    background: red;
    position: relative;
}*/
.notice-heading a, .pds-heading a{
    display: inline-block;
    padding: 0 14px;
    height: 34px;
    background: #333 linear-gradient(to bottom, #ccc, #aaa);
    line-height: 34px;
    border: 1px solid #333;
    border-bottom: #fff;
    border-radius: 5px 5px 0 0;
}
.pds-heading a{
    position: absolute;
    top: 0;
    left: 100px;
}
.notice-heading a:hover, .pds-heading a:hover{
    display: inline-block;
    padding: 0 14px;
    height: 34px;
    background: #fff;
    line-height: 34px;
    color: red;
    border: 1px solid red;
    border-bottom: #fff;
    border-radius: 5px 5px 0 0;
}
.board ul{
    margin: 0;
    padding: 0;
}
.board li{
    background: green;
    list-style: none;
}
.board li a{
    margin-bottom: 30px;
}
.board li::before{
    content:"r";
    font-family: 'webcafeIcon';
}
.board-date{
    float: right;
}
.notice-more, .pds-more{
    position: absolute;
    top: 0;
    right: 0;
}
.notice-more::before,
.pds-more::before{
    content: "p";
    font-family: 'webcafeIcon';
    position: relative;
    top: 2px;
    color: lime;
    margin-right: 3px;
}
```
>놓치고 있는것
>
>1. reset
>   * h2
>   * ul
>   * a
>2. layout
>3. style

> 공지사항, 자료실 탭을 position: absolute로 탑 래프트 지정해주면 되지만 유동적으로 움직일 수 있으니 float: left를 주겠다.
- 다시 짠 css

```css
/* 공지사항 및 자료실 */
.board{
    background: yellow;
    margin-top: 20px;
    position: relative;
    height: 180px;/* 이후에 새소식 단락이 들어오면 겹쳐버리니까 일부러 넣어주는 높이값*/
}
.notice-heading, .pds-heading{
    margin: 0;
    font-size: 1.4rem;
    float: left;
}
a.tab{
    background:#eee linear-gradient(to bottom, #eee, #ccc);
    border: 1px solid #aaa;
    border-radius: 5px 5px 0 0;
    color: #666;
    display: block;
    padding: 5px 10px;
}
.board-active a.tab{
    border-color: #f00 #f00 #fff #f00;
    background: #fff;
    color: #f00;
}
.notice-list, .pds-list, .notice-more, .pds-more{
    display: none;
}
}
.board-active [class$="list"],
.board-active [class$="more"]{
    display: block !important;
}/* 클래스랑 []랑 꼭 띄어써야해!! */
.notice-list, .pds-list{
    margin: 0;
    padding-left: 0;
    list-style: none;
    position: absolute;
    width: 100%;
    top: 40px;
    left: 0;
}
.notice-list li,
.pds-list li{
    margin: 5px 0;
}
.notice-list li::before,
.pds-list li::before{
    content: "r";
    font-family: 'webcafeIcon';
}

.notice-list a,
.pds-list a{
    display: inline-block;
    width: calc(100% - 90px);/* 연산자 기호와 값 사이에 띄어써야해! */
    white-space: nowrap;
    overflow: hidden;/* 독립된 상자가 되면서 안에 컨텐츠가 인라인컨텐츠가 되어서 틈이 생김 */
    text-overflow: ellipsis;
}
.pds-list{
}
.board-date{
    float: right;
}
.notice-more, .pds-more{
    position: absolute;
    top: 0;
    right: -8px;
    padding: 8px;
}
.notice-more::before,
.pds-more::before{
    content: "p";
    font-family: 'webcafeIcon';
    color: yellowgreen;
    position: relative;
    top: 2px;
    margin-right: 3px;
}
```