---
title: "nodeJS"
categories:
  - Server
---

## express
express는 MERN stack 의 server framework이다.  
express framework를 사용하려면 먼저 아래와 같은 코드를 사용해 npm에서 다운로드 받아야 한다.
`npm install expres --save`  

먼저 간단한 exprerss 서버를 만들어서 hello world를 받아 보는 것부터 시작했다.  

```js
const express = require('express')
const app = express();
const PORT = process.env.NODE_ENV === 'production' ? 3001: 3002

app.listen(PORT,()=>{
   console.log(`server listen on ${PORT}`)
})
```  

위의 연습코드에서 `const PORT = process.env.NODE_ENV === 'production' ? 3001: 3002` 해당 부분이 어떤 역할을 하는지 이해가 가지않아 구글에 검색해보았다. => 검색 키워드 : process.env.NODE_ENV  

## NODE_ENV란???
Node.js를 실행할때 NODE_ENV 값을 이용해서 아래와같이 두가지로 나누어 실행하게 되는데
- production(배포) 모드
- development(개발) 모드

Express 프레임워크의 경우 아래와같이 개발에 도움을 줄 수 있는 환경으로 설정을 해준다.
- production 모드 : 파일 캐싱, 에러 메시지 감추기 등 배포의 적합한 환경 설정
- development 모드 : 파일 캐시이 방지, 디버그를 위한 상세한 에러 메시지 보이기 등

## NODE_ENV 값을 설정하는 방법
아래와같은 코드를 터미널에 입력해주면 된다.

  ```
  // Linux, Mac OS X
  export NODE_ENV=모드명
  export NODE_ENV=production
  
  // windows
  set NODE_ENV=production
  ```

NODE_ENV를 설정해주고

```js
// 방법1
if (process.env.NODE_ENV == 'production') {
  console.log("Production Mode");
} else if (process.env.NODE_ENV == 'development') {
  console.log("Development Mode");
}

// 방법2
app.configure('production', function() {
  console.log('production mode);
})
```

위와같이 코드를 작성해주면 __NODE_ENV 값에 따라 개발과 배포용 소스를 따로 분리해서 코딩__할 수 있다.

## 알게된 내용 내코드에 적용시키기

터미널에 `export NODE_ENV=production`이라고 입력한 후 아래와같이 코드를 작성하고 서버를 실행하면

```js
const express = require("express");
const app = express();
const PORT = process.env.NODE_ENV === "production" ? 3001 : 3002;
console.log("현재 모드 : ", process.env.NODE_ENV);

if (process.env.NODE_ENV == "production") {
  console.log("Production Mode");
} else if (process.env.NODE_ENV == "development") {
  console.log("Development Mode");
}

app.listen(PORT, () => {
  console.log(`server listen on ${PORT}`);
});
```
이렇게 콘솔이 찍힌다!

![Screenshot from 2020-02-08 11-44-36.png](https://images.velog.io/post-images/yhe228/03e9c360-4a1d-11ea-a77e-bff20a601eb8/Screenshot-from-2020-02-08-11-44-36.png)


## Hello world 찍어보기

```js
const express = require("express");
const app = express();
const PORT = process.env.NODE_ENV === "production" ? 3001 : 3002;

console.log("현재 모드 : ", process.env.NODE_ENV);

app.get("/", (req, res) => {
  res.send("hello world");
});

app.listen(PORT, () => {
  console.log(`server listen on ${PORT}`);
});
```

hello world가 찍혔다..!
![image.png](https://images.velog.io/post-images/yhe228/1a2d27f0-4a1f-11ea-8ca7-2b1a4558e405/image.png)


## 참고블로그
[Node.js 에서 NODE_ENV 값으로 배포/개발 환경설정하기](https://steemit.com/kr/@inspiredjw/node-js-nodeenv)
[[Node.js Express] 어플리케이션 모드 설정](https://ggmouse.tistory.com/201)
