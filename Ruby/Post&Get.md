## Post와 Get으로 정보 전달하기

### 기본 구조
- request 메세지 -> routes.rb -> params -> Comtroller -> 변수를 이용해서 전달 -> View -> 브라우저

### 정보를 전달하는 방법
- 변수를 이용해서 전달
- form태그로 request 메세지에 담아서 전달
- params 로 읽는다
- URL로 request 메세지에 담아서 전달

### Form태그
- 사용자에게 정보를 받을 때 사용
- 정보들의 묶음
```html
<form metho="post" action="/login">
  <input type="text" name="id">
  <input type="password" name="pw">
  <input type="checkbox" name="remember">
  <input type="submit">
</form>
```
- Rails server(ruby code)
```ruby
params[:id] #=> "kkk@kkk.com"
params[:pw] #=> "helloworld!"
params[:remember] #=> true
```
#### Form 태그의 형태
- Form : 정보를 묶어서 보내는 태그
  - => method : 어떤 방식으로 정보를 전달할지
  - => action : 어디로 정보를 전달할지
- input : 사용자에게 정보를 받는 태그
  - => type : 어떤 종류의 정보를 받을지
  - => name : 정보의 이름

#### Get
- URL 상에 정보가 고스란히 보이게 된다.
- 주소창으로 url 복사를 해서 원하는 페이지로 갈 수 있다.
- 정보가 다 노출되기 때문에 단점
- 보여지지 말아야하는 정보가 url에 노출되지 않게 해야한다.
- 주소창: http://localhost:3000/result?num1=123&num2=12

#### Post
- url 상에 정보를 보여주지 않는다.
- url을 복사해서 이동할 수 없다.
- 만약에 post 방식으로 보내게 된다면

#### URL로 request 보내기
```ruby
get 'plus/:num1/:num2' => 'home#plus'
```
/plus/1/2
params[:num1] #=> '1'
params[:num2] #=> '2'
