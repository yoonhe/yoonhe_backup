---
title: "화살표 함수에서 this"
categories:
  - JavaScript
---

## 1. 일반 함수에서 this
함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정되는 것이 아니고, 함수를 호출할 때 함수가 어떻게 호출되었는지에 따라 this에 바인딩할 객체가 동적으로 결정된다.

```js
function Prefixer(prefix) {
  this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function (arr) {
  // (A) this === pre
  return arr.map(function (x) {
    return this.prefix + ' ' + x; // (B) this === window
  });
};

var pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim']));
```
__(B)에서 this가 window를 가르키는 이유?__  
생성자 함수와 객체의 메소드를 제외한 모든 함수(내부 함수, 콜백 함수 포함) 내부의 this는 전역 객체를 가리키기 때문이다.  

__🧚‍♀️ 콜백 함수 내부의 this가 메소드를 호출한 객체(생성자 함수의 인스턴스)를 가리키게 하려면?__  

```js
Prefixer.prototype.prefixArray = function (arr) {
  return arr.map(function (x) {
    return this.prefix + ' ' + x;
  }.bind(this)); // this: Prefixer 생성자 함수의 인스턴스
};
```

## 2. 화살표 함수의 this
화살표 함수는 함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정된다. 동적으로 결정되는 일반 함수와는 달리 화살표 함수의 this 언제나 상위 스코프의 this를 가리킨다. 이를 Lexical this라 한다.

> 화살표 함수의 this 바인딩 객체 결정 방식은 함수의 상위 스코프를 결정하는 방식인 렉시컬 스코프와 유사하다.

```js
function Prefixer(prefix) {
  this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function (arr) {
  // this는 상위 스코프인 prefixArray 메소드 내의 this를 가리킨다.
  return arr.map(x => `${this.prefix}  ${x}`);
};

const pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim']));
```

- 화살표 함수는 call, applay, bind 메소드를 사용하여 this를 변경할 수 없다.

```js
Dancer.prototype.step = () => {
  setTimeout(this.step.bind(this), this.timeBetweenSteps); // this === window
};	
```

## 3. 화살표 함수를 사용해서는 안되는 경우
### 1) 메소드
화살표 함수로 메소드를 정의하는 것은 피해야 한다.  
메소드로 정의한 화살표 함수 내부의 this는 메소드를 소유한 객체, 즉 메소드를 호출한 객체를 가리키지 않고 상위 컨택스트인 전역 객체 window를 가리킨다.  

- 예시1
  ```js
  // Bad
  const person = {
    name: 'Lee',
    sayHi: () => console.log(`Hi ${this.name}`)
  };

  person.sayHi(); // Hi undefined
  ```
  - 🧚‍♀️ solution - [ES6의 축약 메소드 표현 사용](https://poiemaweb.com/es6-enhanced-object-property#3-%EB%A9%94%EC%86%8C%EB%93%9C-%EC%B6%95%EC%95%BD-%ED%91%9C%ED%98%84)
  
  ```js
  // Good
  const person = {
    name: 'Lee',
    sayHi() { // === sayHi: function() {
      console.log(`Hi ${this.name}`);
    }
  };

  person.sayHi(); // Hi Lee
  ```

### 2) prototype
```js
// Bad
const person = {
  name: 'Lee',
};

Object.prototype.sayHi = () => console.log(`Hi ${this.name}`);

person.sayHi(); // Hi undefined
```
객체의 메소드로 정의하였을 때와 마찬가지로 화살표 함수 내부의 this는 생성자 함수를 호출한 Instance를 가리키지 않고 상위 컨택스트인 전역 객체 window를 가리킨다.  
그러므로 prototype에 메소드를 할당하는 경우에는 아래와 같이 일반 함수를 할당하는 것이 좋은 방법이다.
```js
// Good
const person = {
  name: 'Lee',
};

Object.prototype.sayHi = function() {
  console.log(`Hi ${this.name}`);
};

person.sayHi(); // Hi Lee
```

### 3) 생성자 함수
화살표 함수는 생성자 함수로 사용할 수 없다. 생성자 함수는 prototype 프로퍼티를 가지며 prototype 프로퍼티가 가리키는 프로토타입 객체의 constructor를 사용한다. 하지만 화살표 함수는 prototype 프로퍼티를 가지고 있지 않다.

```js
const Dancer = () => {};

// 화살표 함수는 prototype 프로퍼티가 없다
console.log(Dancer.hasOwnProperty('prototype')); // false

const dancer = new Dancer(); // TypeError: Foo is not a constructor
```

### 4) addEventListener 함수의 콜백 함수
addEventListener 함수의 콜백 함수를 화살표 함수로 정의하면 this가 상위 컨택스트인 전역 객체 window를 가리킨다.

```js
// Bad
var button = document.getElementById('myButton');

button.addEventListener('click', () => {
  console.log(this === window); // => true
  this.innerHTML = 'Clicked button';
});
```
- solution : 일반함수 사용

```js
// Good
var button = document.getElementById('myButton');

button.addEventListener('click', function() {
  console.log(this === button); // => true
  this.innerHTML = 'Clicked button';
});
```

addEventListener 함수의 콜백 함수 내에서 this를 사용하는 경우, function 키워드로 정의한 일반 함수를 사용하여야 한다. 일반 함수로 정의된 addEventListener 함수의 콜백 함수 내부의 this는 이벤트 리스너에 바인딩된 요소(currentTarget)를 가리킨다.

## 내가 이해가 안갔던 코드
```js
Dancer.prototype.step = () => {
  setTimeout(this.step, this.timeBetweenSteps);
};

Dancer.prototype.setPosition = (top, left) => {
  Object.assign(this.$node.style, {
    top: `${top}px`,
    left: `${left}px`
  });
}; 
```

prototype의 메서드로 할당된 화살표 함수 내부의 this는 생성자 함수를 호출한 Instance 객체를 가리키지않고 화살표 함수의 상위 Scope this인 전역객체(window)를 가리킨다.  
그러므로 전역객체(window)에는 $node나 .step이라는 메서드가 없기때문에 에러가 났던 것이다.  


- Solution : 일반 함수를 할당

```js
Dancer.prototype.step = function() {
  setTimeout(this.step.bind(this), this.timeBetweenSteps);
}; 

Dancer.prototype.setPosition = function(top, left) {
  Object.assign(this.$node.style, {
    top: `${top}px`,
    left: `${left}px`
  });
};
```

### 👨‍🏫 [참고블로그](https://poiemaweb.com/es6-arrow-function)

