---
title: "JavaScript에서 Object를 생성하는 여러가지 방법들"
categories:
  - JavaScript
---

## JavaScript에서 Object를 생성하는 여러가지 방법들

1. new Object() 생성자 사용

```js
let fruit1 = new Object();
fruit1.name = 'banna';
```

2. 객체 리터럴({}) 사용

```js
let fruit2 = {name : 'banna'};
```

3. 생성자 함수

```js
let Fruit = function(name) {
	this.name = name;
}

let fruit3 = new Fruit('banna');
```

💁‍♀️ 1,2,3 결과

```js
console.log('fruit1 ? ', fruit1.name)
// fruit1 ?  banna
console.log('fruit2 ? ', fruit2.name)
// fruit2 ?  banna
console.log('fruit3 ? ', fruit3.name)
// fruit3 ?  banna
```
