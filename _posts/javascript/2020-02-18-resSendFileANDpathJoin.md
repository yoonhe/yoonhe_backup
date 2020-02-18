---
title: "res.sendFile & path.join"
categories:
  - Server
---

## static
Express에서 이미지, CSS 파일 및 JavaScript 파일과 같은 정적 파일을 제공

### static 기본 형태
정적 파일이 포함된 디렉토리의 이름을 express.static 미들웨어 함수에 전달하면 파일의 직접적인 제공을 시작한다

```js
app.use(express.static('public'));
app.use(express.static('files')); // 여러 디렉토리를 사용하려면 미들웨어 함수를 여러번 사용한다

// public 디렉토리에 포함된 파일을 로드할 수 있다
http://localhost:3000/images/kitten.jpg
http://localhost:3000/css/style.css
http://localhost:3000/js/app.js
```

### 가상 경로 사용
express.static 함수를 통해 제공되는 파일에 대한 가상 경로를 작성할 수 있다.

```js
app.use('/static', express.static('public'));

// /static 경로를 통해 public 디렉토리에 포함된 파일을 로드할 수 있다.
http://localhost:3000/static/images/kitten.jpg
http://localhost:3000/static/css/style.css
http://localhost:3000/static/js/app.js
```

### node 프로세스 실행 경로
```js
// node 프로세스가 실행되는 디렉토리에 대해 상대적 - 상대경로
app.use(express.static('public'));

// node 프로세스가 실행되는 디렉토리에 대해 절대적 - 절대경로
app.use('/static', express.static(__dirname + '/public'));
```

node 프로세스가 실행되는 디렉토리가 항상 같지 않으므로 절대경로를 사용하면 매번 경로를 정해줄 필요가 없어 편리하다.

```js
// 제로초님 도서의 예시코드를 참고하였습니다

console.log(__filename); // C:\Users\zerocho\filename.js => node 프로세스가 실행되는 현재 파일
console.log(__dirname); // C:\Users\zerocho => node 프로세스가 실행되는 현재 위치

// filename.js 실행
$ node filename.js
```



#### 내코드
```js
// basic-server.js
const express = require("express");
const cors = require("cors");
const parser = require("body-parser");
const routes = require("./routes");
const app = express();

app.use(express.static("client"));
// 이코드를 통해서 client 디렉토리에 포함된 파일을 로드할 수 있다.

app.use(cors());
app.use(parser());
app.use("/", routes);

app.listen(3000, () => {
  console.log("chatterbox-serer listen on 3000");
});

```

## 참고블로그
[[생활코딩]Express-정적파일을 서비스하는 법](https://opentutorials.org/course/2136/11857)
[Express에서 정적 파일 제공](https://expressjs.com/ko/starter/static-files.html)
