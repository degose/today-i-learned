FDS-09-메인컨텐츠3
========

## <<webcafe 실습>>

### 컬럼2 - 탭메뉴(유동적인 방법) / 새소식
---
#### 공지사항, 자료실



~~~css
/* 신규 이벤트 및 관련 사이트 */
.event-related{
    background: yellow;
    background: radial-gradient(tp bottom, #ccc, #eee);
    padding: 12px;
}
.event{
    background: orange;
    position: relative;
}
.event-heading, .related-heading{
    background: blue;
    margin: 0;
    font-size: 1.6rem;
}
.event-heading span, .related-heading span{
    color: #f00;
}
.event-detail{
    background: olive;
}
.event-thumbnail{
    background: purple;
    margin: 13px 0 17px 0;
    display: flex;
    justify-content: space-around;
}
.event-brief{
    background: skyblue;
    margin: 0;
}
.btn-event-group{
    background: red;
    margin: 0;
        position: absolute;
    top: 0;
    right: 0;
     height: 18px;
}
.btn-event-group button{
    background: url(images/back_forward.png) no-repeat;
    display: inline-block;
    border-style: none;
    padding-top: 20px;
    overflow: hidden;
    width: 19px;
    height: 18px;
}
button.btn-event-next{
    background-position: 100% 0;
    margin-left: 5px; 
}
.related{
    background: skyblue;
}
.related-list{
    background: orange;
    margin: 0;
    list-style: none;
    padding: 0;
}
~~~


>처음 스타일을 줄때 




~~~css
.related{
    /*background: skyblue;*/
}
.related-list{
    background: #fff;
    margin: 12px 0 0 0;
    list-style: none;
    padding: 5px 0 5px 27px;
    border: 1px solid #aaa;
    border-radius: 3px;
    height: 20px;
    line-height: 1.5;
    overflow: hidden;
}
ul.related-list:hover{
    list-style: none;
    padding: 6px 0 6px 27px;
    border: 1px solid #aaa;
    height: 110px;
}
~~~


- `transition`

- ul 여기에 줘야함
- ul:hover


transform 책넘어가는 효과 다시해봐라


- 인기 사이트
~~~html
<div class="popular-site">
                    <h2 class="popular-site-heading">인기 <span>사이트</span></h2>
                    <ol class="popular-site-list">
                        <li>
                            <a href="#">W3C</a>
                            <div class="popular-site-up">상승</div>
                        </li>
                        <li>
                            <a href="#">CSS ZEN GARDEN</a>
                            <div class="popular-site-down">하강</div>
                        </li>
                        <li>
                            <a href="#">WEB STANDARDS</a>
                            <div class="popular-site-stay">중단</div>
                        </li>
                        <li>
                            <a href="#">웹 접근성 연구소</a>
                            <div class="popular-site-up">상승</div>
                        </li>
                    </ol>
                    <a href="#" class="popular-site-more" target="_blank" title="인기 사이트">더보기</a>
                </div>
~~~
~~~css
/* 인기 사이트 */
.favorite{
    position: relative;
    padding: 10px;
    margin-top: 20px;
    background: #ccc linear-gradient(to bottom, #eee, #ccc);
    border: 1px solid #aaa;
    border-radius: 5px;
}
.favorite-heading{
    margin: 0;
    font-size: 1.6rem;
    padding: 0;
    background: blue;
}
.favorite-heading span{
    color: #f00;
}
.favorite-list{
    background: pink;
    padding-left: 0;
    /*list-style: none;/* ol 값을 읽어주기 않아 */
    overflow: hidden;
    margin: 0;
    margin-top: 10px;
}
.favorite-list li{
    counter-increment: number;/* 변수처럼 동작 */
    background: olive;
    line-height: 25px;
}
.favorite-list li::before{
    content: counter(number, decimal);/* 이름 / 10진수 */
    background: #aaa;
    border-radius: 2px;
    font-size: 1.2rem;
    color: #fff;
    padding: 2px 7px;
}
.favorite-list em{
    float: right;
    background: #aaa url(images/rank.png) no-repeat;
    width: 9px;
    height: 10px;
    overflow: hidden;
    /*display: inline-block;*/
    /*padding: 10px 0 0 0;*/
    font-size: 0px;
    /*line-height: 17px;*/
    /*margin: 6px 0 0 0;*/
    /*text-align: right;*/
    /*line-height: 50%;*/
    transform: translateY(50%);
}
.favorite-list em.stop{
    /*background-position: 50% 0;*/
    background-position-y: 50%;
}
.favorite-list em.down{
    /*background-position: 50% 0;*/
    background-position-y: 100%;
}
.favorite-more{
    position: absolute;
    top: 10px;
    right: 10px;
}
.favorite-more::before{
    content: "p";
    font-family: 'webcafeIcon';
    color: yellowgreen;
    position: relative;
    top: 2px;
    margin-right: 3px;
}
~~~

~~~css
.box{
    background: pink;
    width: 200px;
    height: 200px;
    transition: transform 1s;
    transform-origin: left top;
}
.box:hover{
    transform: scale(2);   
}

.container{
    background: silver;
    width: 250px;
    height: 250px;
    position: relative;
    perspective: 800px;
}
.card{
    background: darkblue;
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    transform-style: preserve-3d;
    transition: transform 1s;
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
}
.card:hover{
   transform: rotateY(180deg); 
}
.front, .back{
    background: yellow;
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    line-height: 250px;
    font-size: 36px;
    text-align: center;
}
.back{
    background: pink;
    transform: rotateY(180deg);
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
}
  @keyframes spinner {
    from {
      -moz-transform: rotateY(0deg);
      -ms-transform: rotateY(0deg);
      transform: rotateY(0deg);
    }
    to {
      -moz-transform: rotateY(-360deg);
      -ms-transform: rotateY(-360deg);
      transform: rotateY(-360deg);
    }
  }
  .containter2 {
    -webkit-perspective: 1200px;
    -moz-perspective: 1200px;
    -ms-perspective: 1200px;
    perspective: 1200px;
    width: 500px;
  }
 .text-box {
     margin-top: 100px;
     width: 300px;
     background: pink;
    -webkit-animation: spinner linear infinite 3s;
    -moz-animation: spinner linear infinite 3s;
    -ms-animation: spinner linear infinite 3s;
    animation: spinner linear infinite 3s;
    -webkit-transform-style: preserve-3d;
    -moz-transform-style: preserve-3d;
    -ms-transform-style: preserve-3d;
    transform-style: preserve-3d;
  }
.text-box:hover{
    -webkit-animation-play-state: paused;
    -ms-animation-play-state: paused;
    animation-play-state: paused;
}
~~~