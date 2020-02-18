---
title: "res.sendFile & path.join"
categories:
  - Server
---

```js
const express = require("express");
const router = express.Router();
const path = require("path");
const messages = {
  results: []
};

router.get("/view", (req, res) => {
  res.sendFile(path.join(__dirname, "../client", "index.html"));
});

router.get("/classes/messages", (req, res) => {
  res.status(200).send(messages);
});

router.post("/classes/messages", (req, res) => {
  const data = req.body;
  messages.results.push(data);
  res.status(201).send(data);
});

module.exports = router;
```

위의 코드에서 `res.sendFile`과 `path.join`에 대해 두루뭉실할게 알고 사용한 것 같아 다시 정리를 해보려 한다.

### res.sendFile(path, [options], [callback])

 : path의 파일을 읽고 해당 내용을 클라이언트로 전송한다.
 
 ```js
router.get("/view", (req, res) => {
  res.sendFile(path.join(__dirname, "../client", "index.html"));
});
```

- **sendFile** : `/view`로 `get` 요청이 오게되면 `path.join(__dirname, "../client", "index.html")` 해당 경로의 파일을 읽고 내용을 클라이언트로 전송한다.
- **__dirname** : node 프로세스가 실행되는 디렉토리의 절대경로
- **path** : 폴더와 파일의 경로를 쉽게 조작하도록 도와주는 모듈이다
  - 운영체제별로 경로 구분자가 다르기 때문에 필요하다
      - **Windows**: `C:\Users\ZeroCho`처럼 `\`로 구분된다
      - **POSIX**: `/home/zerocho`처럼 `/`로 구분합니다.  
- **path.join**  
  path.join의 인자로 들어온 각각의 스트링을 하나의 경로로 결합한다. 
	
  ```js
  var path = require('path');
  var x = path.join('Users', 'Refsnes', 'demo_path.js');
  console.log(x);

  // x ?
  // Users\Refsnes\demo_path.js
  ```
