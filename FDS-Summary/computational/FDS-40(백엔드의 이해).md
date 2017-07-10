FDS-40-벡엔드의 이해
========

# 백엔드의 이해

## 서버 어플리케이션
- 참고: <http://bsnippet.tistory.com/47>
### 프로세스
### 쓰레드

## Web server vs App server
- 초기 인터넷은 웹 서버 라는 용어로 모든걸 통칭해 사용했지만, 시간이 지나면서 사용자에게 원활한 서비스를 제공하기 위해 기능적인 계층(Layer)를 나누게 되었다. 여기서 웹 서버와 웹 애플리케이션 서버와 차이가 생기게 됐다.
- 웹 서버는 정적인 데이터를 처리하는 서버이다. 이미지나 단순 html파일과 같은 리소스를 제공하는 서버는 웹 서버를 통하면 WAS를 이용하는 것보다 빠르고 안정적이다. WAS는 동적인 데이터를 처리하는 서버이다. DB와 연결되어 데이터를 주고 받거나 프로그램으로 데이터 조작이 필요한 경우에는 WAS를 활용 해야 한다.

### Web server
- 인터넷 상에서 웹 브라우저 클라이언트로부터 HTTP 요청을 받아들이고, HTML 문서와 같은 웹 페이지들을 보내주는 역할을 하는 프로그램. HTTP 요청에 따라 서버에 저장되어 있는 웹페이지를 클라이언트에게 전달하는 것. 웹 페이지 뿐만 아니라 그림, 스타일 시트, 자바스크립트도 해당. 
- 주로 정적 컨텐트(static content) 처리
- Forward Proxy와 Reverse Proxy 지원
- nginx, apache, GWS 등
#### Forward proxy / Reverse proxy
### App server (WAS(Web Application Server))
- 인터넷 상에서 HTTP를 통해 사용자 컴퓨터나 장치에 애플리케이션을 수행해 주는 미들웨어라고 한다. Servlet, ASP, JSP, PHP 등의 웹 언어로 작성된 웹 애플리케이션을 서버단에서 실행된 후 실행 결과값을 사용자에게 넘겨주게 되고, 우리가 가진 브라우져가 결과를 해석해서 화면에 표시하는 순으로 동작을 한다.
- 웹 애플리케이션 서버 3가지 기본 기능
  - 프로그램 실행 환경과 데이터베이스 접속 기능을 제공
  - 여러 개의 트랜잭션을 관리
  - 업무를 처리하는 비즈니스 로직 수행
- 주로 동적 컨텐트 담당
- 아파치 톰캣, 제우스 등
#### CGI(Common Gateway Interface)
- 웹서버를 위한 표준 프로토콜
- 

## Sails.js
- 참고: <http://sailsjs.com/>
- 참고: <http://seokjun.kr/1juilmane-syopingmol-mandeulgi/>
- Node.js 에서 가장 유명한 MVC 프레임워크


## RESTful API
### 묵시적(implict) vs 명시적(explict)

## Route

## ORM(Object Relation Mapping)
- 참고: <http://www.javajigi.net/pages/viewpage.action?pageId=6560>
- 참고: <http://debop.blogspot.kr/2012/02/orm-object-relational-mapping.html>
- 참고: <http://www.javajigi.net/display/OSS/Object-Relational+Mapping+Strategies#Object-RelationalMappingStrategies-ObjectModeling>
- DB query(질의) 물어보면 db가 답해줌
- OOP 언어와 데이터를 다루는 RDBMS 와의 상이한 시스템을 매핑하여, 쉽게 데이터 관련 OOP 프로그래밍을 쉽게 하도록 하기 위한 기술이다. 
- CRUD를 위해 긴 SQL문장을 작성할 필요가 없다.쿼리 작성은 여전히 필요하지만, ORM 툴(HQL 등)을 이용하면 한충 쉽게 만들 수 있다. 또 JDBC와 관련된 복잡한 코드 작업으로부터 해방될 수 있다.
- 관계형 모델과 관련된 성능 오버헤드를 수반하지 않고도 요구사항에 적합한 도메인 모델을 생성할 수 있으며, 로우와 컬럼이 아닌 오브젝트의 관점에서 작업을 수행하는 것이 가능하다.
- 변경 사항을 자동으로 감지하므로, 전체 개발 라이프사이클에 걸쳐 에러의 가능성을 줄일 수 있다.
- 데이타베이스 벤더 별로 제공되는 SQL 구문에 대한 종속성을 줄이고 호환성을 향상시켜 준다. SQL 구문은 ORM 툴에 의해 추상화가 가능하다.



## 도커(docker)
- 참고: <https://gist.github.com/nacyot/8366310>
- 참고: <https://www.docker.com/>
- 컨테이너를 제공하는 소프트웨어 기술
- 추가적인 추상 레이어 및 운영체제 레벨의 가상화의 자동화를 제공한다.
- 가볍고 빠름(일반 가상머신과 비교하여. 아파치 이런 프로그램들은 환경설정하는게 아주 오래걸림)
### 실습 (Docker로 MariaDB 설치)
#### MariaDB Docker로 이미지 만들기
- `$ docker run --name [이미지 이름] -d -v [컴퓨터에 db파일을 저장할 경로]:/data/db -p 3306:3306 -e MYSQL_ROOT_PASSWORD=1234 mariadb`
```bash
$ docker run --name fastcampus_maria_db -d -v /Users/gose/fastcampus/mariadb:/data/db -p 3306:3306 -e MYSQL_ROOT_PASSWORD=1234 mariadb
```
#### 만든 이미지 실행하기
- `docker start [이미지 이름]`
```bash
$ docker start fastcampus_maria_db
```
- hello/config/datastore.js 파일 바꿔주기
```js
adapter: 'sails-mysql',
url: 'mysql://root:1234@localhost:3306/hello',
```
- sails-mysql 설치
```bash
$ npm install sails-mysql --save
```
- sails lift -> 2 -> enter
```bash
$ sails lift
prompt: ?:  2 
```

## DBMS(Database Management System)
- 자료에 대한 사용자의 다양한 요구를 적절히 처리하고 응답해 줌으로써 이를 사용할 수 있도록 해주는 시스템
- 기본용어
  - 스키마(schema)
  - 테이블(table): 표 형식으로의 Data 묶음.
  - 쿼리(query)
  - 뷰(view)
  - 행(row): (레코드) 로의 데이터들이 서로 연관성있는 자료로서 일반적으로 행의 개념을 두고 작업한다.
  - 열(column): (필드) 동일한 성격을 갖는 데이터를 저장하는 열 개념.(성명, 주소...)
  - 기본키(primary key): record를 식별하기 위한 비어있지 않은 유일한 값.
  - 외래키(foreign key): 다른 테이블의 Primary key와 대응되는 필드
  - 데이터형(data type): 각 field에 들어갈 데이터의 형식


## DBeaver
- 받기전에 JAVA SE JDK를 먼저 받자. => 받는 이유? JAVA byte 코드로 되어있는데 이 코드를 JDK 가 실시간으로 기계어로 바꿔준다.
- 참고: <http://dbeaver.jkiss.org/download/enterprise/>

## RDBMS(Relational Database Management System)
### Relational Databases
- 관계형 모델(Relational Model)
  - 구조체(테이블 스키마 지칭)와 1차 술어논리로 구성된 언어(DB에서는 SQL을 지칭)를 사용하여 데이터를 다루는 접근법
- 관계 종류
  1. 일대일
  2. 일대다 / 다대일
  3. 다대다
- Oracle, MySQL, MariaDB, Sybase 등
## SQL(Structered Query Language)
- 구조화된 질의 언어, DB에서 정보를 생성, 혹은 갱신하여 사용할 수 있도록 정의된 표준 언어
- 특정 RDBMS에서만 쓸수 있는 SQL 구문도 존재 하지만 대부분은 공통적으로 쓸 수 있음
- 대소문자 구분 안함
  - 테이블 생성 - CREATE TABLE [테이블 이름] ([컬럼 이름] [자료형], ...);
  - 테이블 삭제 - DROP TABLE [테이블 이름]
  - 입력 - INSERT INTO [테이블 이름]([컬럼 이름], ...) VALUES([입력값], ...);
  - 조회 - SELECT [컬럼이름], ... FROM [테이블 이름] WHERE [조건식]
  - 수정 - UPDATE [테이블 이름] SET [컬럼 이름] = [수정할 값] WHERE [조건식]
  - 삭제 - DELETE [테이블 이름] WHERE [조건]

## 트렌젝션(Transaction)
- 데이터베이스 관리 시스템의 상호작용의 단위
- 논리적 작업 단위(LUW, Logical Units of Work)
- 목적: 데이터베이스 완전성(integrity)유지
- 전부 되거나, 전부 취소 되거나
- COMMIT
- ROLLBACK

## NoSQL
- RDBMS와 다르게 최초 생상시 데이터간 관계를 정의하지 않음(설계시 유연) - 명시적인 스키마가 존재하지 않음
- MongoDB, Redis, HBase 등
- 대용량 웹 서비스를 위하여 만들어진 데이터 저장소
- 관계형 데이터 모델을 지양하며 대량의 분산된 데이터를 저장하고 조회하는데 특화된 저장소
- 스키마 없이 사용 가능하거나 느슨한 스키마를 제공하는 저장소

## RDBMS vs NoSQL 장단점
- 참고: <http://wwst.tistory.com/55>

## REQUEST, RESPONSE
## req
## res
## Middleware
## 레디스(redis)
## view
## EJS(Effective JavaScript Templating)
## GRUNT

