---
title: "객체 지향 프로그래밍"
categories:
  - JavaScript
---

## 객체 지향 프로그래밍

1. 각각의 인스턴스는 해당 클래스의 고유한 속성과 메소드를 갖는다
2. 클래스에 속성과 메소드를 정의하고, 인스턴스에서 이용한다.

```js
// ES6
class Food {
  constructor(name, brand) {
    // 인스턴스가 만들어질 때 실행되는 코드
    this.name = name;
    this.brand = brand;
  }

  eat() {
    return this.name + '을 먹는 중입니다.';
  }
}

let food1 = new Food('홈런볼', '해태제과');
let food2 = new Food('다이제', '닥터유');
food1.name // "홈런볼"
food1.eat() // "홈런볼을 먹는 중입니다."
```

```js
// ES5
function Ramen(name, brand) {
  // 인스턴스가 만들어질 때 실행되는 코드
  this.name = name;
  this.brand = brand;
}

Ramen.prototype.eat = function() {
  return this.name + '을 먹는 중입니다.';
}
let ramen1 = new Ramen('너구리', '농심');
ramen1.name // "너구리"
ramen1.eat() // "너구리을 먹는 중입니다."
```

### 배열을 정의하는 것은 Array의 인스턴스를 만들어내는 것과 동일하다
```js
let arr2 = new Array(1,2,3,4,5);

arr2 // (5) [1, 2, 3, 4, 5]
arr2.push('push num');
arr2 // (6) [1, 2, 3, 4, 5, "push num"]
```

