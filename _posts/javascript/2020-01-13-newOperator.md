---
title: "New Operator"
categories:
  - JavaScript
---

> new 연산자는 사용자 정의 객체 타입 또는 내장 객체 타입의 인스턴스를 생성한다. (MDN)

## new가 하는 일
1. 새로운 빈 객체를 만들어낸다.
2. this를 새로 만들어진 객체에 bind한다.
3. 새로 만들어진 객체에 "__proto__"라 불리는 property를 더한다. 이것은 constructor 함수의 prototype 객체를 의미한다.
4. return this를 함수의 끝에 추가한다. 때문에 객체는 함수로부터 return되어 만들어진 것이다. 


### 예시)

```js
function Fruit(name) {
  this.name = name;
}

let apple = new Fruit('apple');
```

1. 새로운 객체(apple)를 만들어낸다
2. this는 `apple` 객체에 bind된다. 때문에 this에 대한 참조는 `apple`을 향할 것이다. 
3. `__proto__`가 추가된다. `apple.__proto__`는 이제 `Fruit.prototype`을 가리킨다. 
4. 모든 것이 완료된 후에 새로운 apple 객체는 새로운 apple 변수에 return된다.



👨‍🏫 [참고블로그](https://3jun.tistory.com/86)
