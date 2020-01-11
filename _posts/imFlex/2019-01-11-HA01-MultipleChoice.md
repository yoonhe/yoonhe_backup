---
title: "객관식 문제 오답풀이"
categories:
  - Im_Flex
---

## 1차 HA 객관식 문제 오답
### 01 what is the value of `x` after running the code below?
🧚‍♀️ 정답 : 10
```js
// NOTE! we are asking for x not the reuslt (문제는 x의 값을 묻고 있습니다)

var x = 30;

function get(x) {
  return x;
}
function set(value) {
  x = value;
}

set(10);
var result = get(20);
```

너무나 쉬운 문제를 틀려버렸다.. 영어만 보면 긴장을 하는 내가.. result의 값인 20을 답으로 적어버렸다 허허..

### 02 What is the value of `result` after running the code below?
🧚‍♀️ 정답 : 10
```js
var x = 10;

function outer() {
  var x = 20;
  function inner() {
    x = x + 10;
    console.log('inner x ? ', x); // inner x ?  30
    console.log('window x ? ', window.x); // window x ?  10
    return x;
  }
  inner();
  console.log('outer x ? ', x) // outer x ?  30
}

outer();
var result = x;
```

function 안에서 재정의된 변수 x는 전역에 있는 변수 x에 영향을 미치지 않는다.

### 09 What is the `result` after running the code below
🧚‍♀️ 정답 : 30

```js
var obj1 = { x: 10 };
var obj2 = Object.create(obj1);

var obj3 = Object.create(obj2);

obj2.x = 20;

var result = obj3.x + 10; // obj3.x === 20
```

obj3은 obj2를 prototype으로 하는 객체이기 때문에 obj2.x에 20이 할당되었으므로 obj3의 x에 별도의 값이 할당되지 않은 이상 프로토타입 체인을 통해 obj3.x는 obj2.x의 값인 20이 된다.

### 16 After running the code below what message will be eventually be alerted and after how long?
🧚‍♀️ 정답 : Alice says hi, immediately(바로)

```js
var name = 'Window';
var alice = {
  name: 'Alice',
  sayHi: function() {
    alert(this.name + ' says hi');
  }
};
var bob = { name: 'Bob' };

alice.sayHi.bind(bob);

setTimeout(alice.sayHi(), 1000);
```

1초 뒤에 setTimeout을 통해 alice.sayHi가 실행되었다면 this가 window가 되지만 alice.sayHi()로 바로 실행시켜 주었기 때문에 this는 alice가 된다.

### 17 After the following code runs and all setTimeout callbacks run, what will be the value of result?
🧚‍♀️ 정답 : 10

```js
function foo() {
  var data = 10;

  bar(function(players) {
    data = players;
  });

  return data;
}

function bar(callback) {
  setTimeout(callback, 0);
}

var result = foo();
```

setTimeout은 비동기 프로그래밍으로 처리되어서 setTimeout이 실행되기까지 기다리지 않고 바로 아래의 return data를 실행 해준다.


## 느낀점
이번 기회로 잘 모르고 있었던 부분에 대하여 확실하게 짚고 넘어가자 다음엔 헤깔리지 않도록!
