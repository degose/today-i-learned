12-column-layout.css
```css
@charset "utf-8";
body{
    margin: 0;
}
.grid-toggle{
    position: fixed;
    top: 50px;
    right: 50px;
}
.wrapper{
    max-width: 940px;
    margin: 0 auto;
    position: relative;
}
.show-hide-grid::after{
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    background: repeating-linear-gradient(to right, rgba(255,0,0,0.3) 0px, rgba(255,0,0,0.3) 60px, transparent 60px, transparent 80px); 
}
.row::before, .row::after{
    content: "";
    display: block;
    clear: both;
}
.col{
    min-height: 50px;
    width: 100%;
    background: orange;
    margin-bottom: 10px;
    float: left;
    margin-left: 20px;
    position: relative;
}
.alpha{
    margin-left: 0;
}
.omega{
    margin-right: 0;
}
.col-1{
    width: 60px;
}
.col-2{
    width: 140px;
}
.col-3{
    width: 220px;
}
.col-4{
    width: 300px;
}
.col-5{
    width: 380px;
}
.col-6{
    width: 460px;
}
.col-7{
    width: 540px;
}
.col-8{
    width: 620px;
}
.col-9{
    width: 700px;
}
.col-10{
    width: 780px;
}
.col-11{
    width: 860px;
}
.col-12{
    width: 940px;
}
.col-push-0{
    left: 0;
}
.col-push-1{
    left: 80px;
}
.col-push-2{
    left: 160px;
}
.col-push-3{
    left: 240px;
}
.col-push-4{
    left: 320px;
}
.col-push-5{
    left: 400px;
}
.col-push-6{
    left: 480px;
}
.col-push-7{
    left: 560px;
}
.col-push-8{
    left: 640px;
}
.col-push-9{
    left: 720px;
}
.col-push-10{
    left: 800px;
}
.col-push-11{
    left: 880px;
}
.col-pull-0{
    right: 0;
}
.col-pull-1{
    right: 80px;
}
.col-pull-2{
    right: 160px;
}
.col-pull-3{
    right: 240px;
}
.col-pull-4{
    right: 320px;
}
.col-pull-5{
    right: 400px;
}
.col-pull-6{
    right: 480px;
}
.col-pull-7{
    right: 560px;
}
.col-pull-8{
    right: 640px;
}
.col-pull-9{
    right: 720px;
}
.col-pull-10{
    right: 800px;
}
.col-pull-11{
    right: 880px;
}
.col-offset-0{
    margin-left: 0;
}
.col-offset-1{
    margin-left: 100px;
}
.col-offset-2{
    margin-left: 180px;
}
.col-offset-3{
    margin-left: 260px;
}
.col-offset-4{
    margin-left: 340px;
}
.col-offset-5{
    margin-left: 420px;
}
.col-offset-6{
    margin-left: 500px;
}
.col-offset-7{
    margin-left: 560px;
}
.col-offset-8{
    margin-left: 660px;
}
.col-offset-9{
    margin-left: 740px;
}
.col-offset-10{
    margin-left: 820px;
}
.col-offset-11{
    margin-left: 900px;
}
```css


12-column-layout.html
```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>12 컬럼 레이아웃</title>
    <link rel="stylesheet" href="../css/12-column-layout.css">
</head>
<body>
    <button class="grid-toggle" type="button">그리드 보기/감추기</button>
    <div class="wrapper">
        <div class="row">
            <div class="col col-2 alpha">
                컬럼 1
            </div>
            <div class="col col-4 col-offset-4 col-push-2">
                컬럼 2
            </div>
            <div class="col col-2 col-pull-4">
                컬럼 3
            </div>
            <div class="col col-12 alpha">
                컬럼 4
            </div>
        </div>
        <div class="row">
            <div class="col col-11 alpha">
                컬럼
            </div>
            <div class="col col-1">
                컬럼
            </div>
        </div>
        <div class="row">
            <div class="col col-10 alpha">
                컬럼
            </div>
            <div class="col col-2">
                컬럼
            </div>
        </div>
        <div class="row">
            <div class="col col-9 alpha">
                컬럼
            </div>
            <div class="col col-3">
                컬럼
            </div>
        </div>
        <div class="row">
            <div class="col col-8 alpha">
                컬럼
            </div>
            <div class="col col-4">
                컬럼
            </div>
        </div>
        <div class="row">
            <div class="col col-7 alpha">
                컬럼
            </div>
            <div class="col col-5">
                컬럼
            </div>
        </div>
        <div class="row">
            <div class="col col-6 alpha">
                컬럼
            </div>
            <div class="col col-6">
                컬럼
            </div>
        </div>
        <div class="row">
            <div class="col col-5 alpha">
                컬럼
            </div>
            <div class="col col-7">
                컬럼
            </div>
        </div>
        <div class="row">
            <div class="col col-4 alpha">
                컬럼
            </div>
            <div class="col col-8">
                컬럼
            </div>
        </div>
        <div class="row">
            <div class="col col-3 alpha">
                컬럼
            </div>
            <div class="col col-9">
                컬럼
            </div>
        </div>
        <div class="row">
            <div class="col col-2 alpha">
                컬럼
            </div>
            <div class="col col-10">
                컬럼
            </div>
        </div>
        <div class="row">
            <div class="col col-1 alpha">
                컬럼
            </div>
            <div class="col col-11">
                컬럼
            </div>
        </div>
    </div>
    <script src="https://code.jquery.com/jquery-3.2.1.min.js" integrity="sha256-hwg4gsxgFZhOsEEamdOYGBf13FyQuiTwlAQgxVSNgt4=" crossorigin="anonymous"></script>
    <script>
        $(function(){
            $(".grid-toggle").on("click", function(){
                $(".wrapper").toggleClass("show-hide-grid");
            });
        });
    </script>
</body>
</html>
```

isolate-layout.html
```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>isolate Layout</title>
    <link rel="stylesheet" href="../css/isolate-layout.css">
</head>
<body>
    <div class="wrapper">
        <div class="row">
            <div class="col col-12">
                컬럼
            </div>
        </div>
        <div class="row">
            <div class="col col-11 col-offset-1">
                컬럼
            </div>
            <div class="col col-1">
                컬럼
            </div>
        </div>
        <div class="row">
            <div class="col col-4 col-offset-8">
                컬럼 1
            </div>
            <div class="col col-4">
                컬럼 2
            </div>
            
        </div>
        <div class="row">
            <div class="col col-9">
                컬럼
            </div>
            <div class="col col-3 col-offset-9">
                컬럼
            </div>
        </div>
        <div class="row">
            <div class="col col-8">
                컬럼
            </div>
            <div class="col col-4 col-offset-8">
                컬럼
            </div>
        </div>
        <div class="row">
            <div class="col col-7">
                컬럼
            </div>
            <div class="col col-5 col-offset-7">
                컬럼
            </div>
        </div>
        <div class="row">
            <div class="col col-6">
                컬럼
            </div>
            <div class="col col-6 col-offset-6">
                컬럼
            </div>
        </div>
        <div class="row">
            <div class="col col-5">
                컬럼
            </div>
            <div class="col col-7 col-offset-5">
                컬럼
            </div>
        </div>
        <div class="row">
            <div class="col col-4">
                컬럼
            </div>
            <div class="col col-8 col-offset-4">
                컬럼
            </div>
        </div>
        <div class="row">
            <div class="col col-3">
                컬럼
            </div>
            <div class="col col-9 col-offset-3">
                컬럼
            </div>
        </div>
        <div class="row">
            <div class="col col-2">
                컬럼
            </div>
            <div class="col col-10 col-offset-2">
                컬럼
            </div>
        </div>
        <div class="row">
            <div class="col col-1">
                컬럼
            </div>
            <div class="col col-11 col-offset-1">
                컬럼
            </div>
        </div>
    </div>
</body>
</html>
```

isolate-layout.css
```css
@charset "utf-8";

body{
    padding: 50px;
}
.wrapper{
    width: 80%;
    margin: 0 auto;
}
.row::after{
    content: "";
    display: table;
    clear: both;
}
.alpha{
    padding-left: 0;
}
.omega{
    padding-right: 0;
}
.col{
    min-height: 50px;
    width: 100%;
    float: left;
    margin-bottom: 20px;
    background: rgba(255, 0, 0, 0.3);
    margin-right: -100%;
    box-sizing: border-box;
    padding: 0 10px;
    border: 1px solid blue;
}
.col-1{
    width: calc((100% / 12) * 1);
}
.col-2{
    width: calc((100% / 12) * 2);
}
.col-3{
    width: calc((100% / 12) * 3);
}
.col-4{
    width: calc((100% / 12) * 4);
}
.col-5{
    width: calc((100% / 12) * 5);
}
.col-6{
    width: calc((100% / 12) * 6);
}
.col-7{
    width: calc((100% / 12) * 7);
}
.col-8{
    width: calc((100% / 12) * 8);
}
.col-9{
    width: calc((100% / 12) * 9);
}
.col-10{
    width: calc((100% / 12) * 10);
}
.col-11{
    width: calc((100% / 12) * 11);
}
.col-12{
    width: calc((100% / 12) * 12);
}

.col-offset-1{
    margin-left: calc((100% / 12) * 1);
}
.col-offset-2{
    margin-left: calc((100% / 12) * 2);
}
.col-offset-3{
    margin-left: calc((100% / 12) * 3);
}
.col-offset-4{
    margin-left: calc((100% / 12) * 4);
}
.col-offset-5{
    margin-left: calc((100% / 12) * 5);
}
.col-offset-6{
    margin-left: calc((100% / 12) * 6);
}
.col-offset-7{
    margin-left: calc((100% / 12) * 7);
}
.col-offset-8{
    margin-left: calc((100% / 12) * 8);
}
.col-offset-9{
    margin-left: calc((100% / 12) * 9);
}
.col-offset-10{
    margin-left: calc((100% / 12) * 10);
}
.col-offset-11{
    margin-left: calc((100% / 12) * 11);
}
```
negative-margin.css
```css
@charset "utf-8";

body{
    margin: 50px;
}
.text-shadow{
    background: yellow;
    font-size: 60px;
}
.box-wrapper{
    width: 200px;
}
.text-box{
    /*background: pink;*/
    color: red;
    font-size: 10px;
    /*margin-top: -100%;*/
    /*margin-left: ;*/
}

.wrapper{
    margin-top: -10px;
    width: 500px;
    height: 500px;
    background: pink;
    border: 2px solid #000;
    overflow: hidden;
}

.wrapper [class^="box"]{
    width: 50%;
    height: 50%;
    float: left;
    background: darkgreen;
    border: 10px solid red;
    color: #fff;
    font-size: 30px;
    text-align: center;
    margin-left: -10px ;

    margin-right: -10px;
}
.box1{
    /*margin-left: 0;*/
}
.box2{
    /*margin-left: 100px;*/
}
.box3{
    /*margin-left: 200px;*/
}
.box4{
    /*margin-left: 300px;*/
}
```





