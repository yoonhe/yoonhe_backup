---
title: "JavaScript에서 Object를 생성하는 여러가지 방법들"
categories:
  - JavaScript
---

## JavaScript에서 Object를 생성하는 여러가지 방법들(Instantiation Patterns)

### 1. Functional

```js
let Car = function() {
  let someInstance = {};
  someInstance.position = 0;
  someInstance.move = function() {
    this.position ++;
  }
  return someInstance;
}

let car1 = Car();
car1.move()
car1.position // 1
```

position 초기값을 정해줄 수도 있다

```js
let CarType2 = function(position) {
  let someInstance = {};
  someInstance.position = position;
  someInstance.move = function() {
    console.log(this); 
    this.position ++;
  }
 
  return someInstance;
}

let car2 = CarType2(10);
car2.move() // {position: 10, move: ƒ}
```

Functional 방식은 인스턴스를 생성할 때마다 모든 메소드를 someInstance에 할당해서 각각의 인스턴스들에 해당하는 메소드의수 만큼의 메모리를 더 차지하게 된다.

### 2. Functional Shared

```js
let extend = function(to, from) {
  for(let key in from) {
    to[key] = from[key];
  }
}

let someMethods = {};
someMethods.move = function() {
  this.position ++;
}

let Car = function(position) {
  let someInstance = {
    position : position,
  }
  
  extend(someInstance, someMethods);
  return someInstance;
}

let car1 = Car(10);
car1.move();
car1 // {position: 11, move: ƒ}
```

Functional Shared 방식을 사용하면 someMethods 라는 객체에 있는 메소드들의 메모리 주소만을 참조하기 때문에 메모리 효율이 좋아진다.


![image.png](https://images.velog.io/post-images/yhe228/7bfbcff0-18e1-11ea-b484-7d4e953d68fb/image.png)

### 3. Prototypal

```js
let someMethods = {};
someMethods.move = function() {
  this.position ++;
}

let Car = function(position) {
  let someInstance = Object.create(someMethods);

  someInstance.position = position;
  return someInstance;
}

let car1 = Car(10);
car1.move();
car1 // {position: 11}
```
Object.create() 메서드는 지정된 프로토타입 객체 및 속성(property)을 갖는 새 객체를 만들어준다.

### 4. Pseudoclassical

```js
let Car = function(position) {
  this.position = position;
}

Car.prototype.move = function() {
  this.position ++;
}

let car = new Car(5);
```

![image.png](https://images.velog.io/post-images/yhe228/e450ba00-18e3-11ea-b856-7f9c87a20e1c/image.png)

Car 의 프로토타입을 car가 참조하였다.





💁‍♀️ [참고블로그](https://velog.io/@cyranocoding/JavaScript에서의-OOP-Inheritance와-Prototype-Chain과-Class-에-대한-개념-정리-및-이해-spjypizora)


