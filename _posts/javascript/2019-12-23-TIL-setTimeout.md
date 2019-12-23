---
title: "setTimeout - 비동기프로그래밍"
categories:
  - JavaScript
---
오늘 6번째 checkpoint를 풀다가 결과값이 왜 이렇게 나오는지 아무리봐도 이해가 안가는 문제가 있어 구글링을 해보았다.

일단, 내가 이해 안갔던 문제
```js
function foo () {

  var data = 10;

  bar(function (players) {
    data = players;
  });

  return data;
}

function bar (callback) {
  setTimeout(function () {
    callback(20);
  }, 500);
}

var result = foo(); // result === 10
```
- 내가 잘못 알았던 사실
	- callback(20)이 0.5초 후에 실행되고 callback 실행이 끝나면 `return data`를 실행한다
- 구글링 후 알게된 사실
	- `return data`를 먼저 실행하고 0.5초 후에 callback(20)을 실행한다.
    
💁‍♀️ 동기 프로그래밍과 비동기 프로그래밍의 차이였다. 바로 아래에 예시와 함께 동기와 비동기 프로그래밍의 차이를 적어  놓았다.

### 1. 동기 프로그래밍
- 어떤 작업을 요청한 후 그 작업이 완료되기까지 기다렸다가 응답을 받아 처리하는 것을 말한다.

```js
function foo () {

  var data = 10;

  bar(function (players) {
    data = players;
  });

  return data;
}

function bar (callback) {
  callback(20);
}

var result = foo(); // resultl === 20
```

### 2. 비동기 프로그래밍
- 어떤 작업을 요청한 후 다른 작업을 수행하다가 이벤트가 발생하면 그에 대한 응답을 받아 처리하는 것을 말합니다.

```js
function foo () {

  var data = 10;

  bar(function (players) {
    data = players;
  });

  return data;
}

function bar (callback) {
  setTimeout(function () {
    callback(20);
  }, 500);
}

var result = foo(); // result === 10
```

💁‍♀️ [참고 블로그](https://beomy.tistory.com/10)



