FDS-08-메인컨텐츠2(탭메뉴/새소식)
========



## <<참고링크>>
- CssZengarden: 같은 마크업 다양한 css활용
<http://www.csszengarden.com/>
- ARIA UI <https://github.com/niawa/ARIA>
---
---
## <<새로 배운 속성>>
### min-height

최소 높이 (지정한 높이값보다 줄어들더라도 높이값이 유지된다.)

**Syntax**
~~~
min-height : length | % | inherit;
~~~

**예시**
```css
.board{
    min-height: 170px;
}
```


---
---
## <<webcafe 실습>>

### 컬럼2 - 탭메뉴(유동적인 방법) / 새소식
---
#### 공지사항, 자료실

지난시간에 float, position으로 레이아웃을 짰지만 list가 많아지면 board로 고정 높이값 영역을 list가 넘어가버린다.

- 고정적인 레이아웃
```css
/* 게시판 영역 */
.board{
    position: relative;
    height: 180px;/* 높이 값 */
}
/* 탭 */
.notice-heading, .pds-heading{
    float: left;
}
/* 글 리스트 */
.notice-list, .pds-list{
    margin: 0;
    padding-left: 0;
    position: absolute;
    width: 100%;
    top: 40px;
    left: 0;
}
.notice-list a,
.pds-list a{
    display: inline-block;
    width: calc(100% - 90px);
    white-space: nowrap;
}
/* 날짜 */
.board-date{
    float: right;
}
/* 더보기 버튼 */
.notice-more, .pds-more{
    position: absolute;
    top: 0;
    right: 0;
}
```

- 리스트 개수가 7개일 때 (유동적인 레이아웃) css
```css
/* 게시판 영역 */
.board{
    position: relative;
    min-height: 170px;/* 최소 높이 (아무리 줄어들더라도 170px 유지 */
}
/* 탭 */
.notice-heading, .pds-heading{
    margin: 0;
    top: 0;
    position: absolute;
}
.notice-heading{
    left: 0;
}
.pds-heading{
    left: 74px;/* 공지사항 탭 width값 만큼 */
}
/* 글 리스트 */
.notice-list a,
.pds-list a{
    display: inline-block;
    width: calc(100% - 90px);
    white-space: nowrap;
    overflow: hidden;/* 독립된 상자가 되면서 안에 컨텐츠가 인라인컨텐츠가 되어서 틈이 생김 */
    text-overflow: ellipsis;
}
/* 날짜 */
.board-date{
    float: right;
}
/* 더보기 버튼 */
.notice-more, .pds-more{
    position: absolute;
    top: 0;
    right: 0;
}
```
---

#### 새소식

- 내가 짠 마크업(div,p 태그사용)

```html
<div class="news">
    <h2 class="news-heading">새소식</h2>
    <div class="news-list">W3C 사이트가 리뉴얼 되었습니다.
        <time class="board-date" datetime="2017-05-10">2017.05.10</time>
        <p>디자인 및 다양한 view환경을 고려하여 구성되어 있으며, 기존보다 최신 정보 및 개발자를 위한 기술 가이드도 찾기 쉽도록 구성되어 있습니다. </p>
    </div>
    <img src="images/news.gif" alt="W3C 리뉴얼">
    <p>W3C 리뉴얼</p>
    <a href="#" class="news-more" title="새소식" target="_blank">더보기</a>
</div>
```
- 내가 짠 마크업(dl,dd,dt 태그 사용)
```html
<div class="news">
    <h2 class="news-heading">새소식</h2>
    <dl class="news-list">
        <dt>W3C 사이트가 리뉴얼 되었습니다.</dt>
        <time class="board-date" datetime="2017-05-10">2017.05.10</time>
        <dd>
            <img src="images/news.gif" alt="W3C 리뉴얼">
            <p>W3C 리뉴얼</p>
        </dd>
        <dd>
            디자인 및 다양한 view환경을 고려하여 구성되어 있으며, 기존보다 최신 정보 및 개발자를 위한 기술 가이드도 찾기 쉽도록 구성되어 있습니다.
        </dd>
    </dl>
    <a href="#" class="news-more" title="새소식" target="_blank">더보기</a>
</div>
```

- 논리적 구조설계
>1. 새소식
>2. W3C 사이트가~~
>3. 날짜
>4. 기사내용
>5. 썸네일
>6. 더보기

![Alt text](./images/FDS08-01.jpeg)

- 새로 짠 마크업

```html
<div class="news">
    <h2 class="news-heading">새소식</h2>
    <a href="#" class="news-article">
        <article class="news-item">
            <h3 class="news-item-heading">W3C 사이트가 리뉴얼 되었습니다.</h3>
            <time class="news-item-date" datetime="2017-05-11T14:33:25">2015.05.11</time>
            <p class="news-item-brief">디자인 및 다양한 view환경을 고려하여 구성되어 있으며, 기존보다 최신 정보 및 개발자를 위한 기술 가이드도 찾기 쉽도록 구성되어 있습니다. </p>
            <figure>
                <img src="images/news.gif" alt="W3C가 HTMS5를 발표하면서 새롭게 홈페이지를 리뉴얼 했습니다.">
                <figcaption>W3C 리뉴얼</figcaption>
            </figure>
        </article>
    </a>
    <a href="#" class="news-more" target="_blank" title="새소식">더보기</a>
</div>
```
>article태그는 독립적으로 활용할 수 있어서 안에 h1태그를 사용할 수 있다. (본문에서는 h1을 사용해도 자동으로 h3이 적용된다.)

- 내가 짠 css
```css
.news{
    background: yellow;
    position: relative;
    margin-top: 20px;

}
.news-heading{
    margin: 0;
    color: red;
    font-size: 1.6rem;
}
.news-heading::after{
    content: "";
    background: #ccc;
    background:linear-gradient(to right, #ccc, #fff );
    height: 1px;
    width: 380px;
    display: block;/* 가상요소는 인라인요소니까 블럭으로 바꿔줘야지 바보새끼 */
    margin: 14px 0 20px 0; 
}
.news-article{
    padding-top: 20px;
}
.news-item{
    background: pink;
}
.news-item-heading{
    background: lime;
    margin: 0;
    float: right;
    width: 245px;
    text-indent : -17px;
}
.news-item-heading::before{
    content: "r";
    font-family: 'webcafeIcon';
}
.news-item-date{
    background: red;
    float: right;
    width: 245px;
}
.news-item-brief{
    background: blue;
    margin: 0;
    float: right;
    width: 245px;
}
.news-item figure{
    /*background: orange;s*/
    margin: 0;
    /*float: left;*/
    position: absolute;
    box-shadow: 5px 5px 0 #000;
}
.news-item figcaption{
    width: 112px;
    text-align: center;
}
.news-more{
    background: lime;
    position: absolute;
    top: 0;
    right: 0;
}
.news-more::before{
    content: "p";
    font-family: 'webcafeIcon';
    color: yellowgreen;
    position: relative;
    top: 2px;
    margin-right: 3px;
}
```

- 새로 짠 css
```css
/* 새소식 */
.news{
    position: relative;
    margin-top: 20px;
}
.news::before{
    content:"";
    width: 80%;
    height: 1px;
    background:#ccc linear-gradient(to right, #ccc, #fff );
    position: absolute;
    top: 30px;
    left: 0;

}
.news-heading{
    margin: 0;
    color: red;
    font-size: 1.6rem;
}
.news-article{
    display: block;
}
.news-item{
    margin-top: 30px;
    padding-left: 130px;
    position: relative;
}
.news-item-heading{
    margin: 0;
    font-size: 1.4rem;
    margin-top: -3px;
    position: relative;
}
.news-item-date, .news-item-brief{
    padding-left: 1em;
}
.news-item-heading::before{
    content: "r";
    font-family: 'webcafeIcon';
    position: relative;
    top: 2px;
}
.news-item-date{
    display: block;
    margin: 5px 0;
}
.news-item-brief{
    margin: 0;
    line-height: 1.5;
}
.news-item figure{
    margin: 0;
    position: absolute;
    top: 0;
    left: 0;
    text-align: center;
}
.news-item img{
    box-shadow: 0 15px 10px 5px rgba(0,0,0,0.3);
    margin-bottom: 15px;
}
.news-more{
    position: absolute;
    top: -8px;
    right: -8px;
    padding: 8px;
}
.news-more::before{
    content: "p";
    font-family: 'webcafeIcon';
    color: yellowgreen;
    position: relative;
    top: 2px;
    margin-right: 3px;
}
```
### 신규 이벤트 / 관련 사이트

- 내가 짠 마크업

```html
<div class="event">
    <h2 class="event-heading">신규 <span>이벤트</span></h2>
    <a href="#" class="event-item">
        <img src="images/free_gift.gif" alt="웹표준 핵심 가이드북 증정 이벤트" class="event-item-img">
        <p class="event-item-brief">웹표준 핵심 가이드북2 출시! 선착순 500명 한정으로 증정.</p>
    </a>
    <button type="submit" class="btn-event-before">이전 사이트 보기</button>
    <button type="submit" class="btn-event-next">다음 사이트 보기</button>
    <h2 class="site-heading">관련 <span>사이트</span></h2>
    <ul class="site-list">
        <li a href="#">생산성 본부</li>
        <li a href="#">W3C</li>
        <li a href="#">웹 접근성 연구소</li>
        <li a href="#">멀티 캠퍼스</li>
        <li a href="#">CSS Zengarden</li>
    </ul>
</div>
```

- 논리적 구조설계
>1. 신규 이벤트
>2. 이벤트 내용(이미지+텍스트)
>3. 버튼
>4. 관련 사이트
>5. 목록

- 새로 짠 마크업
```html
<div class="event-related">
    <div class="event">
        <h2 class="event-heading">신규 <span>이벤트</span></h2>
        <div id="event-detail">
            <p class="event-thumbnail">
                <img src="images/free_gift.gif" alt="웹표준 핵심 가이드북2" class="event-item-img">
            </p>
            <p class="event-brief">
                <em>웹표준 핵심 가이드북2 출시!</em>선착순 500명 한정으로 증정.
            </p>
        </div>
        <div class="btn-event-group">
            <button type="button" class="btn-event-before">이전 이벤트 보기</button>
            <button type="button" class="btn-event-next">다음 이벤트 보기</button>
        </div>
    </div>
    <div class="related">
        <h2 class="related-heading">관련 <span>사이트</span></h2>
        <ul class="related-list">
            <li><a href="#">패스트캠퍼스</a></li>
            <li><a href="#">웹 접근성 연구소</a></li>
            <li><a href="#">CSS Zengarden</a></li>
            <li><a href="#">W3C</a></li>
            <li><a href="#">Web Standard</a></li>
        </ul>
</div>
```

-  
```html
```
---
---

## ARIA를 활용한 Tab UI

- `role` : 특정 요소(element)에 역할을 정의 / 부여된 역할은 동적으로 변화할 수 없다.
- `properties`, `states` : 속성과 상태는 "aria-*"접두어를 가진다.

참고링크 <https://github.com/niawa/ARIA>
```html
<body>
    <div class="tab-interface">
        <!-- 텝 인덱스 -->
        <ul class="tab-list" role="tablist">
            <li 
            role="tab" 
            id="tab1" 
            aria-selected="true" 
            tabindex="0"
            aria-controls="section1"
            >공지사항</li>
            <li 
            role="tab" 
            id="tab2" 
            aria-selected="flase" 
            tabindex="0"
            aria-controls="section1"
            >자료실</li>
        </ul>
        <!-- 텝 콘텐츠 -->
        <section id="section1" 
        role="tabpanel"
        aria-labelledby="tab1"
        ><p>공지사항 영역입니다.</p></section>
        <section id="section2" 
        role="tabpanel"
        aria-labelledby="tab2"
        ><p>자료실 영역입니다.</p></section>
    </div>
</body>
```
