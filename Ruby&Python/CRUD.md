## CRUD
- Create / Read / Update / Delete

## CR
### model
- 모델을 생성하기 : rails generate model Post
  - 모델 파일 : 중급자용
  - 마이그레이션 파일
  - 테스트 파일
#### 마이그레이션 파일
- 실제 데이터를 넣을 형식을 결정하는 파일
- 짧은 문자열 => String
- 긴 문자열 => text
- 숫자 => integer
- 참/거짓 => boolean
#### 구조
- Controller: app/controller 안에 def 명령어로 액션을 생성한다.
- View: app/view/post 에 생성한 액션과 같은 이름의 erb 파일을 만든다.
- Model: 
  - rails g model Post
  - config/migrate폴더의 migration 파일을 수정한다.
  - rake db:migrate (이런식으로 표를 만들어줘)

- 필요한 페이지
  - 글 작성 Form 페이지
  - 글 생성 action(view는 필요없음)
  - 글 읽기 페이지

- 경로
  - 인풋 요소들로 데이터 작성 후 제출버튼 -> Controller
    - create라는 액션을 생성한다.(view는 안만든다)
  - Controller (model아 저장해) -> Model
    - form을 작성하고 확인 버튼을 누르면 params 안에 정보를 담아서 controller에서 전달받는다.
    - 데이터 저장 명령어
    - post = Post.new
    - post.title = params[:title]
    - post.content = params[:content]
    - post.save
    - id / title / content
  - home/index -> Controller -> Model -> Controller -> View -> 브라우저

#### 모델 생성
```bash
$ rails generate model post
```
- 파일 경로: db -> migrate -> 파일이름
- 테이블 생성
```bash
$ rake db:migrate
```

## UD
- redirect_to "url", redirect_to :back
- 새로운 Model 메소드
  - Post.find(params[:post_id]) => 찾다
  - Post.destroy(params[:post_id]) => 그 열을 삭제
  - id : 유일한 그 post 값
  - Created_at : 이 열이 생성 된 일시
  - Updated_at : 이 열이 바뀌게 되면 그 일시

### 구조
#### Model
- rails g model Post
- config/migrate 폴더의 migration 파일을 수정한다.
- rake db:migrate => migration 완성

#### Controller
- app/controller 안에서 def 명령어로 액션을 만든다.
#### View 
- app/view/post 에 생성한 액션과 같은 이름의 erb 파일을 만든다.

#### 구성
- /update => 글 수정 action (view 필요 없음)
- /modify => 글 수정 form
- /delete => 글 삭제 action (view 필요 없음)

### Update
- /update/:post_id
- create와 유사하나 Controller 부분이 다름
```ruby
def update
  # Post는 지역변수
  post = Post.find(params[:post_id])
end
```
- 특정 데이터를 수정해야 하기 때문에 유일한 값만 갖는 id로 column을 찾는다.
- id 값을 받기 위해 url을 이용한다
```ruby
post 'update/:id' => 'home#update'
```
- routes.rb에 위와같이 작성하면, :id 위치에 적혀진 값을 읽어서 params[:id] 값으로 controller에 넘겨준다.

### Delete
- update와 유사
- form 태그로 정보 교환이 없고 바로 url로 접근하면 해당 데이터가 삭제된다.
```ruby
get 'delete/:id' => 'home#delete'
```
- 여기서 get으로 하는 이유는 a 태그로 링크를 누르기 위함.