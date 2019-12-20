---
title: "Subclassing"
categories:
  - JavaScript
---
# Subclassing 
객체 지향 프로그래밍(OOP)의 Polymorphism과, Inheritance의 개념을 이해하는 것이 중요

## Prototype Chain
Student에서 Human의 Prototype에 있는 sleep 메소드를 사용하려면?  

### 잘못된 방법 - 1
✍ `john.__proto__ = Human.prototype;`

```js
function Human() {}
Human.prototype.sleep = function() {
  console.log('zzz');
}
function Student() {}
Student.prototype.learn = function() {
  console.log('런코')
}
let john = new Student();

john.__proto__ = Human.prototype;
```
`__proto__`는 참조하는 용도로만 사용해야 한다.

### 잘못된 방법 - 2
✍ `Student.prototype = Human.prototype`

```js
function Human() {}
Human.prototype.sleep = function() {
  console.log('zzz');
}
function Student() {}
Student.prototype.learn = function() {
  console.log('런코')
}

Student.prototype = Human.prototype
let john = new Student();
Student.prototype.learn = function() {}
// Human.prototype.learn = function() {}을 해주는 것과 같다.
```
Student의 prototype에 Human의 prototype을 참조하는 것이기 때문에 아래와 같은 문제가 발생한다.
1. Student의 원래 prototype에 있던 sleep 메소드가 사라진다.
2. 이문제를 해결하기 위해 Student의 prototype에 다시 learn 메소드를 추가하면
3. 현재 Student의 prototype은 Human의 prototype의 주소값을 참조한 것이기 때문에 Human에도 learn 메소드가 생겨버린다..!

![image.png](https://images.velog.io/post-images/yhe228/3e0c7c10-22fc-11ea-843c-d3bb12b555d1/image.png)


같은 모양을 가졌지만 다른 reference를 가진 객체를 어떻게 하면 만들수 있을까?

### 좋은 방법 
✍ `Student.prototype = Object.create(Human.prototype);`

> - MDN
Object.create() 메서드는 지정된 프로토타입 객체 및 속성(property)을 갖는 새 객체를 만듭니다. 

```js
let Human = function(name) {
  this.name = name;
}

Human.prototype.sleep = function() {
  console.log('zzz');
}	

let Student = function(name) {
  // this.name => new키워드를 사용해 만든 객체의 this는 instance가 되는데 그 instance를 가리키는 this가 human까지 연결이 안되기 때문에 human의 this가 undefined가 된다.
  Human.call(this, name); // Human.apply(this, arguments);
}

Student.prototype = Object.create(Human.prototype);
Student.prototype.constructor = Student;
// Human.prototype을 프로토타입으로 갖는 새 객체를 만들어 Student.prototype에 넣어주었기 때문에 constructor도 Human을 바라보고 있어서 변경해줄 필요가 있다.
Student.prototype.learn = function() {console.log('learn coding')}

let daeun = new Student('daeun');
daeun.learn(); // learn coding
daeun.sleep(); // zzz
```

![image.png](https://images.velog.io/post-images/yhe228/e1551350-2301-11ea-8ab9-9bbd55681081/image.png)

### class keyword 사용
prototype을 사용하는 것보다 class keyword를 사용하는 것이 더 간단하다.

```js
class Human {
  constructor(name) {
    this.name = name
  }
  sleep() {console.log('zzzz')};
}

class Student extends Human {
  constructor(name) {
    super(name)
  } // 상속을 받아온 Class와 constructor 구조가 같다면 상속 받은 Class에서 생략가능하다.
  learn() {console.log('learn coding')};
}

let heaeun = new Student('heaeun');
heaeun.sleep(); // zzzz
heaeun.learn(); // learn coding
```

![image.png](https://images.velog.io/post-images/yhe228/09570d10-2305-11ea-b2ee-734d4de9b184/image.png)


## 객체지향 다형성 - Polymorphism
### 메소드 확장

```js
function Human(name) {
  this.name;
}

Human.prototype.sleep = function() {console.log('zzzz')}

function Student(name) {
  Human.apply(this, arguments);
}

Student.prototype.sleep = function() {
   Human.prototype.sleep.apply(this); 
   console.log('자면안되요!');
}

let heaeun = new Student('heaeun');
heaeun.sleep();
// zzzz
// 자면안되요!
```

class version
```js
class Human {
  constructor(name) {
    this.name = name;
  }

  sleep() {console.log('zzz')}
}

class Student extends Human {
  sleep() {
    super.sleep() + console.log('자면안되!!!') 
  }
}
let heaeun = new Student('heaeun');

heaeun.sleep();
// 자면안되!!!
// zzz
```

💁‍♀️ [참고블로그](https://poiemaweb.com/js-prototype)
💁‍♀️ [MDN - super](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/super)




