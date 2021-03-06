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
$ cd FDS04_Summary(master)
$ git pull upstream master
$ git push origin master(내 깃허브로 옮기기)
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


# 팀프로젝트 github사용

## collabo
- 사용할 유저들 메일을 등록 (소수의 프로젝트일 때)
- 브랜치 관리가 중요
- 개발용 브랜치(파랑색) 실무에서는 기능별로 브랜치를 딴다.
- 자기이름 브랜치를 따로 따서 작업하는 것도 방법
- 자기 브랜치로 푸시 -> 데브브랜치로 머지
- 같은 파일을 수정을 한 것은 오류남
```bash
$ git checkout dev
$ git checkout -b gose 
$ git push origin gose
$ git pull upstream dev
$ 
```
- 자기 브랜치로 자기 파일 업데이트 잘 하면 되는데, VUE같은 경우에는 파일을 따로 관리하기 때문에 괜찮지만 만약에 여러명이 같은 파일을 수정했을 경우 오류가 발생
```bash
$ git checkout master
$ git pull origin master
$ git pull origin gose
```
- 파일 어떻게 다른지 확인, 어떤 것을 살릴지 정한 후 나머지 오류 메세지, 버릴 코드 삭제 후 푸시


## .git 삭제
```bash
$ rm -rf .git
```

## 저장소 만든 뒤 클론
```bash
$ git clone URL
```

## 브랜치 만들기
```bash
$ git branch user-signup
```
## 삭제하기
```bash
$ git branch -rd origin/master
```

## 파일 만들기
```bash
$ touch 파일이름
```
## 파일 복사?
```bash
$ git fetch??
```

## pull requests
- 
```bash
$
```

## 가져오기
```bash
$ git pull origin
```

## vi text 작성
- insert에서 나가기
- esc 
- :w 
- :wq
```bash
$ vi text.txt
$ 
```

## 로컬에서 충돌된 것 해결하기
- 
```bash
$ git pull origin master
```

## commit 수정하기
- 하지만 절대 push한 commit을 삭제하거나 수정하면 안된다.
- 그럴 경우에는 그냥 새로운 커밋 내용을 push하는 것이 낫다
- push하기 전에 로컬에서 수정하자
```bash
$ git rebase -i
$ 
```

## origin or upstream
- 
```bash
$ git remote add upstream [원본 저장소의 주소]
$ git pull upstream master
```
- 
```bash
$ git pull upstream master
```