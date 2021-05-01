---
title: "매개변수"
categories:
  - JavaScript
---

# 매개변수

Created: May 1, 2021 3:53 PM
Tags: Javascript
image: %E1%84%86%E1%85%A2%E1%84%80%E1%85%A2%E1%84%87%E1%85%A7%E1%86%AB%E1%84%89%E1%85%AE%20d4321234006b443dabe8437439799231/JS.jpeg

## 매개변수

---

### Rest Parameter

정해지지 않은 갯수의 인수를 배열로 나타낼 수 있게 합니다.

```jsx
function getMaxNum(...nums) {
  console.log(nums);
}

getMaxNum(21,10,55,20,100) // (5) [21, 10, 55, 20, 100]

```

### Spread 연산자 (Spread Operator)

연산자의 대상 배열 또는 이터러블(iterable)을 `개별` 요소로 분리한다.

```jsx
let arr = [7, 35, 2, 8, 21];

Math.max(...arr) // 35
```

## arguments

arguments 객체를 통해 인자값을 확인

### 유사 배열 객체

간단하게 순회가능한(iterable) 특징이 있고 length 값을 알 수 있는 특징이 있는 것이다. 즉, 배열처럼 사용할 수 있는 객체를 말한다.

```jsx
function getMaxNum() {
  console.log(arguments)
}

getMaxNum(21,10,55,20,100) // Arguments(5) [21, 10, 55, 20, 100, callee: ƒ, Symbol  (Symbol.iterator)  : ƒ]
```

### 매개변수에 기본값 설정하기

Default Parameter를 할당해줄 수 있다(문자열/숫자/객체 등 어떤한 타입도 가능)

```jsx
function yoon(firstName, lastName = 'heaeun') {
  return firstName + ' ' +lastName;
}

yoon('Kim') // "Kim heaeun"

```

```jsx
function yoon(firstName = 'Yoon', lastName) {
  return firstName + ' ' +lastName;
}

yoon(undefined, 'heaeun') // "Yoon heaeun"
// 중간에 기본 매개변수가 들어가는 경우,
// undefined를 넘겨줬을 때 기본값으로 처리함.
```

옛날에 쓰던 방법 ) 

```jsx
function timeTogoHome(distance, speed) {
  distance = distance || 2000;
  return distance / speed;
}
timeTogoHome(undefined, 10) // 200
timeTogoHome(200, 10) // 20
```
