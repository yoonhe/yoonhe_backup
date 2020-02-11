---
title: "[Express 프레임워크] send메소드와 end메소드의 차이점&작동방식"
categories:
  - Server
---

## ❓ 내가 궁금했던점 ❓ 

아래의 코드를 보고,

fetch에서 `get` 요청을 하게되면 서버에서 데이터를 문자열로 주기때문에 `resp.json()`를  통해 자바스크립트 오브젝트로 바꿔준다고 이해했다.

```js
    fetch: callback => {
            window
              .fetch(app.server)
              .then(resp => {
                return resp.json();
              })
              .then(callback);
          },
```

아래와같이 `http 모듈` 사용시에는 `messages`를  `JSON.stringify(messages)` 를 통해 문자열로 바꿔서 응답을 해주고

```js
    const messages = {
      results: [
        {
          username: "Jono",
          text: "Do my bidding!",
          roomname: "코드스테이츠"
        }
      ]
    };
    
    if (request.method === "GET") {
    		if (request.url === "/classes/messages") {
    			const data = JSON.stringify(messages);
    // get 요청 시 results 객체를 클라이언트에 stringify 후 전달합니다.
    			response.end(data);
    		} else {
    			status = 404;
    			response.writeHead(status, defaultCorsHeaders);
    			response.end();
    		}

``` 

`express framework` 사용시에는 `send(messages)` 를 통해 응답을 해주는데 `send(messages)` 안에 http 모듈에서 object를 문자열로 바꿔주기위해 사용했던 `JSON.stringify(messages)` 와 같은 기능이 포함되어있는지가 궁금했다.

```js
    const messages = {
      results: [
        {
          username: "Jono",
          text: "Do my bidding!",
          roomname: "코드스테이츠"
        }
      ]
    };
    
    router.get("/classes/messages", (req, res) => {
      res.status(200).send(messages);
    });
```

[Express res.json과 res.send 비교](https://haeguri.github.io/2018/12/30/compare-response-json-send-func/)글을 통해 나의 궁금점을 해결할 수 있었다.

### `res.json` 소스코드 분석

`res.json`은 내부적으로 `res.send` 를 호출하고 있었다는 사실을 알게되었다..!

```js
    res.json = function json(obj) {
      var val = obj;
    
      // 생략...
    
      var app = this.app;
      var escape = app.get('json escape')
      var replacer = app.get('json replacer');
      var spaces = app.get('json spaces');
      var body = stringify(val, replacer, spaces, escape)
    
      if (!this.get('Content-Type')) {
        this.set('Content-Type', 'application/json');
      }
    
      return this.send(body);
    };
```

1. `res.json`의 인자로 obj를 받는다
2. obj는 `stringify`를 통해 JSON 문자열로 변환된다
3. 변환된 `obj`는 `body`에  할당된다
4. `Content-Type` 헤더가 세팅되지 않았을 경우 `this(res 객체)` 에 `Content-Type` 으로 `application/json`을 세팅한다.
5. `res.send(body)` 를 실행하여 결과값을 반환한다.

### `res.send` 소스코드 분석

    res.send = function send(body) {
        var chunk = body;
    
        // 생략....
    
        switch (typeof chunk) {
            // string defaulting to html
            case 'string':
                if (!this.get('Content-Type')) {
                    this.type('html');
                }
                break;
            case 'boolean':
            case 'number':
            case 'object':
                if (chunk === null) {
                    chunk = '';
                } else if (Buffer.isBuffer(chunk)) {
                    if (!this.get('Content-Type')) {
                        this.type('bin');
                    }
                } else {
                    return this.json(chunk);
                }
                break;
        }
    
        // 생략..
    
        return this;
    }

1. `res.send` 함수의 인자로 `body`를 받는다
2. `body` 는 바로 `chuck`에  할당된다
3. switch문을 통해 `chunk` 에 대한 타입검사가 진행된다.
    1. `chunk`가 `object`타입이면 `res.json`을 호출한다.

3-1. 여기서 의문, 계속해서 서로를 호출하면 스택이 넘쳐버리지 않을까??

1. res.send(object)로 코드를 실행했을 때 함수의 실행 순서
    1. res.send(object)
    2. res.json(object)
    3. res.send(string)
2. `res.send`의 인자의 타입이 `object`일때 `res.json` 을 호출하면 `res.json` 에서 문자열로 바꿔서 다시 `res.send` 의 인자로 넣고 호출하게 되는데 `res.send`에서 인자가 `string` 일 경우에는 `object` 일 때와 다른 분기를 타게되서 `res.json` 을 호출하지 않는다. 그렇기때문에 스택이 넘칠일은 없다..!

### 참고 블로그
- [Express res.json과 res.send 비교](https://haeguri.github.io/2018/12/30/compare-response-json-send-func/)

