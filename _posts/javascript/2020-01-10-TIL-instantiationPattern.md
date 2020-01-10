---
title: "instantiation pattern 장단점"
categories:
  - JavaScript
---

인스턴스화 패턴은 JavaScript로 무언가를 만드는 방법이다. JavaScript는 객체를 생성하는 4가지 방법을 제공하는데 어떤 방법을 사용하든 모든 방법은 다음과 같은 기능을 제공한다.  
- object 생성
- object에 methods 및 properties 생성

JavaScript에는 아래와 같이 네가지 instantiation pattern이 있다.  
1. Functional
2. Functional-shared
3. Prototypal
4. Pseudoclassical

## Functional Instantiation
1. 함수를 만든다  
2. 함수 내에서 빈 객체를 만들고 속성과 메소드를 추가한 후 객체를 return 한다.

```js
let Food = function(name) {
  let obj = {};
  
  obj.name = name;
  obj.eat = function() {
    console.log(`${obj.name}을 먹는 중입니다.`)
  }
  
  return obj;   
}

let food1 = Food('라면');

food1.eat(); // 라면을 먹는 중입니다.
```

1. 장점 
	- 이해하기 쉽다.
2. 단점
	- 모든 메서드가 함수에 내에 포함되어 있어서 매번 인스턴스를 생성할 때마다 메모리에 메소드를 복제한다.
    - 메소드를 수정 한 후 새 오브젝트를 작성하면 원래 오브젝트와 새 오브젝트가 다른 메소드를 참조한다.
    

## Functional Shared Instantiation
1. 함수를 만든다  
2. 함수 내에서 빈 객체를 만들고 속성을 정의한다.  
3. 메소드는 다른 객체에 정의해준 후 함수 내의 객체에서 주소값만 참조해준다.  

```js
let extend = function(to, from) {
  for(let key in from) {
    to[key] = from[key]
  }
}

let Food = function(name) {
  let obj = {};
  
  obj.name = name;

  extend(obj, method) // point!!!
  
  return obj;   
}

let method = {
  eat : function() {
    console.log(`${this.name}을 먹는 중입니다.`)
  }
}

let food1 = Food('라면'); // 라면을 먹는 중입니다.
```

1. 장점 
	- 메소드의 중복을 제거하여 메모리 관리를 향상시킨다.
2. 단점
	- 메소드를 수정 한 후 새 오브젝트를 작성하면 원래 오브젝트와 새 오브젝트가 다른 메소드를 참조한다.


## Prototypal Instantiation
prototype chain을 사용하여 객체를 만든다.(Object.create 사용)
1. 별도의 객체에 모든 method를 작성한다.
2. 함수를 만든다.
3. 함수 안에서 Object.create 메소드를 사용하여 메소드를 참조한다.
4. 함수 내부의 속성을 정의 한 후 객체를 return 한다.

```js
let Food = function(name) {
  let obj = Object.create(method); // point!!!
  
  obj.name = name;
  
  return obj;   
}

let method = {
  eat : function() {
    console.log(`${this.name}을 먹는 중입니다.`)
  }
}

let food1 = Food('라면');
```

1. 장점
	- 메서드는 객체 내에서 반환되지 않고 개체의 프로토 타입에 연결된다
    - __모든 메소드는 메모리에서 메소드를 복제하지 않고__ 작성된 모든 오브젝트에서 사용할 수 있다.
2. 단점
	- 메소드를 사용하려면 객체를 정의하고 method를 가지고 있는 객체를 prototype으로 하는 객체를 만들어 정의한 객체에 할당해준 다음 생성자 함수에서 리턴해줘야 한다.
    
## Pseudoclassical Instantiation
1. 함수를 만든다
2. `this` 키워드를 사용하여 속성을 정의한다.
3. method는 prototype에 정의한다.
4. 인스턴스 객체를 만들때에는 `new` 키워드를 사용한다.

```js
let Food = function(name) {
  this.name = name; // this 키워드 사용 
}

Food.prototype.eat = function() {
  console.log(`${this.name}을 먹는 중입니다.`)
}

let food1 = new Food('라면'); // new 키워드 사용
ƒ () {
  console.log(`${this.name}을 먹는 중입니다.`)
}
food1.eat(); // 라면을 먹는 중입니다.
```

1. 장점
	- Pseudoclassical Instantiation는 JavaScript에 내장 된 기능을 활용한 가장 최적화 된 객체 생성 방법이다
2. 단점
	- 디자인이 조금 복잡하다

💁‍♀️ [참고블로그](https://medium.com/dailyjs/instantiation-patterns-in-javascript-8fdcf69e8f9b)
