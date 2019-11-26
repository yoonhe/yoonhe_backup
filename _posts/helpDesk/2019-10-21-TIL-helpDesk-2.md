---
title: "[Help Desk] 프로토타입 상속 관련 문제"
categories:
  - JavaScript
---

## 프로토타입 상속
https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/Inheritance <br>
위의 reference, mdn에서 inheritance를 구현하는 방식을 알아보았다.

```js
function Person(first, last, age, gender, interests) {
  this.name = {
    first,
    last
  };
  this.age = age;
  this.gender = gender;
  this.interests = interests;
};

Person.prototype.greeting = function() {
  alert('Hi! I\'m ' + this.name.first + '.');
};

function Teacher(first, last, age, gender, interests, subject) {
  // Person() 상속
  Person.call(this, first, last, age, gender, interests);

  this.subject = subject;
}
```

Teacher() 생성자는 Person()의 메소드를 상속받지 못한 상태이다. 

```js
Object.getOwnPropertyNames(Person.prototype) // ["constructor", "greeting"]
Object.getOwnPropertyNames(Teacher.prototype) // ["constructor"]
Teacher.prototype.greeting // undefined
```

그래서 아래와 같은 코드를 추가해준다.

```js
Teacher.prototype = Object.create(Person.prototype);
// Person.prototype 객체를 가지고 있는 새 객체를 생성하여 Teacher.prototype으로 할당

Teacher.prototype.greeting;
/*
  ƒ () {
    alert('Hi! I\'m ' + this.name.first + '.');
  }
*/
```
Person.prototype에 정의된 모든 메소드를 사용할 수 있게 되었다..!

하지만 Teacher.prototype의 constructor 속성이 Person()으로 되어있으면 문제의 소지가 있어서 <br>
고쳐주어야 하므로 아래의 코드를 추가한다.

* Teacher.prototype의 constructor 속성이 Person()이 된 이유 
  - Teacher.prototype에 Person.prototype을 상속받은 객체를 할당했기 때문

```js
Teacher.prototype.constructor = Teacher;
```

![image](https://user-images.githubusercontent.com/53102889/67208543-ab4caa00-f450-11e9-90e1-6a1ff20d8992.png)

## Teacher.prototype.constructor = Teacher 코드를 추가하는 이유 ?

* inheritance : 상속
  - 한단계의 inheritance라면, 문제가 되지 않는다.
  - 다만, 연속되는 inheritance chaining이 구현되기 위해서는 constructor를 자기자신으로 지정해 주어야한다
  - new 생성자로 생성되는 instance는 constructor 함수를 이용해서 생성되는데 만약 위와같은 Teacher.prototype.constructor = Teacher 코드가 없는 경우라면, 다음의 inheritance에 문제가 생길것이다.

## Teacher에 새 greeting() 함수 부여하기

```js
Teacher.prototype.greeting = function() {
  alert('hello, world');
};
/*
ƒ () {
  alert('hello, world');
}
*/
```

## 질문에 답변해 주신 개발자분의 solution

  javascript에서는 OOP 구현을 위해 prototype을 이용해 힘들게, inheritance를 구현한다고 생각했어요.<br>
  javascript ES6 문법인 class 에 대해서 알아보시는 방향이 더 좋을 것 같습니다.<br>
  라는 말씀을 해주셨다.
  
  - [프로토타입 상속 관련](https://poiemaweb.com/js-prototype) 
  - [help desk 게시글 복사내용](https://github.com/yoonhe/TIL/issues/1) 
