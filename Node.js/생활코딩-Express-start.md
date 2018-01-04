# 생활코딩 Node.js & Express - Express-start


## 설치
- 링크: http://expressjs.com/ko/
```bash
$ npm init
$ npm install --save express
```

## 라우팅
- app.js
```js
const express = require('express');
const app = express();

// 라우팅
// locallhost:3000/
app.get('/', (req, res) => {
  res.send('Hello home page');
});
// locallhost:3000/login
app.get('/login', (req, res) => {
  res.send('Please login page');
});

app.listen(3000, () => {
  console.log('Connected 3000 port!');
});
```