---
title: "JavaScript에서 Object를 생성하는 여러가지 방법들"
categories:
  - JavaScript
---

## JavaScript에서 Object를 생성하는 여러가지 방법들

### 1. 객체 리터럴({}) 사용

```js
let fruit2 = {name : 'banna'};
```

객체 리터럴은 중괄호('{}')로 객체를 직접 정의하는 방법을 말한다. 위와 같이 객체가 정의 되는 순간. 객체는 프로토타입(Prototype)으로 Object.prototype을 가진다. 따라서 Object.prototype 에 정의된 메소드들을 사용할 수 있다. 

### 2. 생성자 함수

```js
function Fruit(name) {
  this.name = name;
}

Fruit.prototype.eat = function() {
  console.log(this.name + '를 먹습니다.')
}

let banna = new Fruit('banna');

banna.eat() // banna를 먹습니다.
```

constructor 함수를 만들고 new 키워드로 객체를 생성할 수 있다. 
new로 생성된 banna 객체는 Fruit의 프로토타입에 접근 할 수 있다

### 3. Object.create

```js
let fruitPrototype = {
  eat : function() {
    console.log(this.name + '를 먹습니다.'); 
  }
}

let Fruit = function(name) {
  let instance = Object.create(fruitPrototype);
  instance.name = name;
  return instance;
}

let banna =  Fruit('banna');
banna.eat() // banna를 먹습니다.
```

Object.create 메소드는 인자로 들어온 객체를 프로토타입으로 하는 새로운 객체를 생성한다. 위의 예제에서 fruitPrototype 이라는 객체를 인자로 넣었으므로, banna의 프로토타입 객체는 fruitPrototype 이 된다. 따라서 Constructor Function 을 사용한 것처럼, 프로토 타입 객체와 연결이 가능하다.

💁‍♀️ [참고블로그](https://velog.io/@cyranocoding/JavaScript에서의-OOP-Inheritance와-Prototype-Chain과-Class-에-대한-개념-정리-및-이해-spjypizora)


