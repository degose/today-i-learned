# github 저장소 내려받기(git clone)
---
- 해당 github페이지에서 오른쪽 clone 버튼에 url카피
```bash
 $ git clone (url)
```
여기서! checkout 4th 브런치로 해줘야 해당파일들이 보인다.

# github 저장소 바뀐 내용 내려받기(git pull)
- FDS04_Summary 내려받기
```bash
$cd FDS04_Summary(master)
$git pull upstream master
$git push origin master(내 깃허브로 옮기기)
```
- 야무쌤 수업 내용 최신버전 동기화
```bash
$ git remote -v
$ git remote add upstream https://github.com/yamoo9/FDS.git
$ git remote -v
$ git pull upstream 4th
$ git push origin 4th
```

# 내 작업 github에 올리기(git push)
```bash
$ git init (저장소 만들기)
$ git (url)
$ git push (저장소 이름) (master)
$ git remote v
```

# 작업한 것을 올리고 싶다면
```bash
$ git add *
$ git commit -am "어떤것을 작업했다"
$ git remote -v
$ git push (저장소 이름) (master)
```


# && (명령어를 또 만들고 싶을 때)
```bash
$mkdir images &&
 touch index.html css/modules/init.css
```

# node-sass
- 설치 확인
```bash
$ node -v
v7.10.0
```
- json파일 만들고 그 안에 {} 넣기
```bash
$ echo '{}' > package.json
```
```bash
$ node-sass sass/ -o css/ --source-map true
$ node-sass --watch sass/ -o css/ --source-map true
$ node-sass sass/ -o css/ --output-style expanded --source-map true
```
노드사스를 불러올건데, sass폴더 하위에 있는건데, 아웃풋은 css/폴더에 있는거 할거야
아웃풋 스타일은 익스펜디드로 할거고, 소스맵은 개발자 도구에 오른쪽에 scss파일 어느 줄에 스타일이 있는지 알려주는 도구야

## node-sass 전역설치(global)
```bash
$ npm ls node-sass -g
```

## node-sass 지역설치
```bash
$ npm install --save-dev node-sass
```
이렇게 하면 package.json 안에 아래처럼 들어감
```bash
{
  "devDependencies": {
    "node-sass": "^4.5.3"
  }
}
```

# 도움말
```bash
$ node-sass --help
```

# sass 스크립트 단축키
package.json파일 안에 script단축키를 만들었다.
```bash
{
  "scripts": {
    "sass" : "node-sass --output-style expanded css/modules/grid.scss > css/modules/grid.css",
    "watch" : "npm run sass -- -w"
  },
  "devDependencies": {
    "node-sass": "^4.5.3"
  }
}
```
```bash
$ npm run sass
> @ sass /Users/gose/FDSme/LECTURE/DAY02/yuyu.com
> node-sass --output-style expanded css/modules/grid.scss > css/modules/grid.css
$ npm run watch
> @ sass /Users/gose/FDSme/LECTURE/DAY02/yuyu.com
> node-sass --output-style expanded css/modules/grid.scss > css/modules/grid.css
```
!!!! 이 명령어들은 꼭!! package.json파일이 보이는 폴더에서 실행해야 된단다..
나올때는 contl + c


# git에 올릴때 node_modules는 올리면 안된다.
<https://www.gitignore.io/>
.gitignore 파일을 만들고 상단 사이트에서 osx / node / sass / visualcode / 넣고 검색한 코드들 복사 붙여넣기




npm init -y


# github에서 작업한 html 바로 열기

```bash
$ cd webtest(해당폴더)
$ git init
$ git remote -v
$ git remote add origin https://github.com/degose/webtest.git(해당 저장소 url복붙)
$ git remote add origin
$ git add .
$ git commit -m "first commit"
$ git push origin master
$ git checkout -b gh-pages
$ git push origin gh-pages

```
주소창에 degose.github.io/webtest(저장소 이름 / 여러개 가능 경로만 잘 만들면)
https://degose.github.io/FDS-Practice/layout-position/ 이런식으로 만들어야 함

- master브랜치에서 작업 후 gh-pages merge시키기
```bash
$ git push origin master (master)
$ git checkout gh-pages (gh-pages)
$ git merge master 
$ git push origin gh-pages
```

# 실수로 gh-pages로 작업했는데 master로 옮기고 싶을때
당황하지 마르구.. gh-paghes로 작업된(수정된)파일을 다른데 복사해 두었다가 
git checkout master로 바꾼뒤
master 폴더에 복사해뒀던 파일들을 다시 넣어서 push 하면 된단다....