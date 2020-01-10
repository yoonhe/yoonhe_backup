---
title: "접미사/접두사 연산자 👉🏻 증가 (++)"
categories:
  - JavaScript
---

## 증가 연산자(++)의 특징
- 접미사로 사용되면 증가하기 전에 값을 반환한다.
- 접두사로 사용되면 증분 후 값을 반환한다.


### 예시1)
```js
let a = 5   // 5
let b = a++ // 5
let c = a   // 6
```
b에 a의 value인 5가 할당되고 그 후에 a가 증가(++) 된다.

```js
let a = 5   // 5
let b = ++a // 6
let c = a   // 6
```
a가 증가(++)된 후에 b에 a가 증가(++)된 값인 6이 할당된다.


### 예시2)
접미사로 사용되었을때,  
1. obj[count] = val를 실행한다.
2. count를 증가(++) 시켜준다.

```js
let count = 0;
let obj  = {};

function add(val) {
  obj[count++] = val
}

add(3)
console.log(obj) // {0: 3} 
```

접두사로 사용되었을때,  
1. count를 증가(++) 시켜준다.
2. obj[count] = val를 실행한다.

```js
let count = 0;
let obj  = {};

function add(val) {
  obj[++count] = val
}

add(3)

console.log(obj) // {1: 3}
```

💁‍♀️ [참고 블로그](https://riptutorial.com/ko/javascript/example/761/%EC%A6%9D%EA%B0%80--plusplus-)
