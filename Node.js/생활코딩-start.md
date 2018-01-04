# 생활코딩 Node.js & Express - start

## 실행
- hello.js
```js
console.log('Hello world');
```
- bash
```bash
$ node hello.js
Hello world
```
## 서버 실행
- webserver.js
```js
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```
- bash
```bash
$ node webserver.js
Server running at http://127.0.0.1:3000/
```

## 인터넷의 동작 방법
- 서버 / 클라이언트 / IP / port

### 서버 & 클라이언트
- `클라이언트`(요청) - 인터넷 - `서버`(응답)
- `http://a.com` => 도메인
- 52.192.173.151 => IP주소

### 서버
- `http://a.com` 이라는 서버가 있을 때 그 안에 여러개의 서버들 중 무엇을, 어떻게 응답할 수 있느냐?
  - 데이터베이스 서버
  - 채팅 서버
  - 게임 서버
  - 웹 서버

### PORT
- 0 ~ 65535 개의 port
- 80 -> 웹 서버(80번 포트를 웹서버가 듣는다.) `http://a.com:80` -> 하지만 도메인뒤에 늘 :80이라고 적지 않고 생략할 수 있다.
- 만약 `http://a.com:1337`로 연결하고 싶다면 -> 1337번 포트에 웹서버를 연결하면 된다.
