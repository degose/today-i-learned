html-02(form)
========
### 생활코딩 html강의 - <https://opentutorials.org/course/2039/10955>

## form
- 사용자에게 입력을 받을 수 있는 태그
- 아래 예시에서 아이디와 주소의 경우 name값을 적어주지 않으면 구분할 수 없다.(서버에 각각의 name값으로 전달)
```html
<html>
<head>
  <meta charset="utf-8">
</head>
<body>
<form action="http://localhost/login.php">
  <p>아이디 : <input type="text" name="id"></p>
  <p>비밀번호 : <input type="password" name="pwd"></p>
  <p>주소 : <input type="text" name="address"></p>
  <input type="submit">
  <!-- 제출 버튼 -->
</form>
</body>
</html>
```

### text
```html
<html>
<head>
  <meta charset="utf-8">
</head>
<body>
  <form action="">
    <p>text : <input type="text" name="id" value="default value"></p>
    <p>password : <input type="password" name="pwd" value="default value"></p>
    <p>textarea :
      <textarea cols="50" rows="2">default value</textarea>
    </p>
  </form>
</body>
</html>
```

### 선택
#### dropdown list
- multiple : 컨트롤키를 누르고 선택하면 여러개 선택 가능 (하지만 좋은 UI는 아니다.)
```html
<html>
  <head>
    <meta charset="utf-8">
  </head>
  <body>
    <form action="http://localhost/color.php">
      <h1>색상</h1>
      <select name="color">
        <option value="red">붉은색</option>
        <option value="black">검은색</option>
        <option value="blue">파란색</option>
      </select>
      <h1>색상2 (다중선택)</h1>
      <select name="color2" multiple>
        <option value="red">붉은색</option>
        <option value="black">검은색</option>
        <option value="blue">파란색</option>
      </select>
      <input type="submit">
    </form>
  </body>
</html>
```
#### radio
- 단일 선택
- name값이 같은 것들끼리 그룹핑이 된다.
- checked : 페이지가 열렸을 때 기본적으로 선택 되어지는 것
```html
<html>
  <head>
    <meta charset="utf-8">
  </head>
  <body>
    <form action="http://localhost/order.php">
      <p>
        <h1>색상(단일선택)</h1>
        붉은색 : <input type="radio" name="color1" value="red">
        검은색 : <input type="radio" name="color1" value="black" checked>
        파란색 : <input type="radio" name="color1" value="blue">
      </p>
      <p>
        <h1>색상(단일선택)</h1>
        붉은색 : <input type="radio" name="color2" value="red">
        검은색 : <input type="radio" name="color2" value="black" checked>
        파란색 : <input type="radio" name="color2" value="blue">
      </p>
      <input type="submit">
    </form>
  </body>
</html>
```

#### checkbox
- 다중 선택
```html
<html>
  <head>
    <meta charset="utf-8">
  </head>
  <body>
    <form action="http://localhost/order.php">
      <p>
        <h1>사이즈(다중선택)</h1>
        95 : <input type="checkbox" name="size" value="95">
        100 : <input type="checkbox" name="size" value="100" checked>
        105 : <input type="checkbox" name="size" value="105" checked>
      </p>
      <input type="submit">
    </form>
  </body>
</html>
```

### 버튼
```html
<html>
<head><meta charset="utf-8"></head>
<body>
  <form action="http://localhost/form.php">
    <input type="text">
    <input type="submit" value="전송">
    <input type="button" value="버튼" onclick="alert('hello world')">
    <input type="reset">
  </form>
</body>
</html>
```

### hidden field (데이터 전송)
- 서버로 데이터를 전송하는데 UI가 필요 없거나, 몰래 데이터를 전송해야 될 때
```html
<html>
  <head>
    <meta charset="utf-8">
  </head>
  <body>
    <form action="http://localhost/hidden.php">
      <input type="text" name="id">
      <input type="hidden" name="hide" value="egoing">
      <input type="submit">
    </form>
  </body>
</html>
```

### label
```html
<html>
  <head>
    <meta charset="utf-8">
  </head>
  <body>
    <form action="http://localhost/hidden.php">
      <label for="text">text</label>
      <!-- 아래 id input과 연결됨 -->
      <input id="text"type="text" name="id">
      <label>
        <input type="hidden" name="hide" value="egoing">
      </label>
      <input type="submit">
    </form>
  </body>
</html>
```

### method(방법)
- 데이터를 어떤 방법으로 전송할 것인가?
- 어떠한 경우에는 url로 전달해야 할 때가 있고, 감춰서 전달해야 할 때가 있다.
- `method="get"` : url로 전송 (기본)
- `method="post"` : 숨겨서 전송 - 100% 포스트 방식으로 전달하는것이 좋다.
- 서버쪽 엔지니어의 요청이 있을 때에만 지정해서 작업해야 한다.
```html
<html>
  <head>
    <meta charset="utf-8">
  </head>
  <body>
    <form action="http://localhost/method.php" method="post">
      <input type="text" name="id">
      <input type="password" name="pwd">
      <input type="submit">
    </form>
  </body>
</html>
```

### 파일 업로드
- `enctype="multipart/form-data"`
```html
<html>
  <head>
    <meta charset="utf-8">
  </head>
  <body>
    <form action="http://localhost/upload.php" method="post" enctype="multipart/form-data">
      <input type="file" name="profile">
      <input type="submit">
    </form>
  </body>
</html>
```

### input 새로운 type
- 사용자의 입력을 제한할 수 있다.
- 사용자가 유효하지 않은 값을 입력하게 되면 알아서 경고창이 뜸
- `color`  
- `date` 
- `datetime` 
- `datetime-local`  
- `email` 
- `month` 
- `number`: <input type="number" min="10" max="15"> => 모바일 환경에서 키보드를 열면 숫자를 입력할 수 있는 화면이 뜨게 함
- `range`
- `search`
- `tel`
- `time`
- `url`
- `week`

### 입력양식
- `autocomplete="on"` : 입력했던 값을 기억해줌
- `autofocus` : 웹페이지가 열렸을때 자동으로 사용자의 커서가 포커싱되게 하는것.
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
  </head>
  <body>
    <form action="login.php" autocomplete="on">
      <input type="text" name="id" placeholder="id를 입력해주세요." autofocus>
      <input type="password" name="password" autocomplete="off" placeholder="비밀번호를 입력해주세요.">
      <input type="submit">
    </form>
  </body>
</html>
```

### 입력값 체크
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
  </head>
  <body>
    <form action="register.php">
      <input type="text" name="id" placeholder="아이디를 입력" required pattern="[a-zA-Z].+[0-9]">
      <input type="email" name="email" placeholder="이메일 입력">
      <input type="submit">
    </form>
  </body>
</html>
```