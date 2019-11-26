---
title: "[Help Desk] reduce 함수 관련 문제"
categories:
  - JavaScript
---

오늘 내 질문글에 친절하게 답변을 해주신 개발자님 덕분에 reduce 함수에 대해 흐지부지하게 알고있던 부분에 대해 다시한번 되짚어보는 좋은 시간을 가지게 되었다.

```js
let products;

products = [
  { name: "Sonoma", ingredients: ["artichoke", "sundried tomatoes", "mushrooms"], containsNuts: false },
  { name: "Pizza Primavera", ingredients: ["roma", "sundried tomatoes", "goats cheese", "rosemary"], containsNuts: false },
  { name: "South Of The Border", ingredients: ["black beans", "jalapenos", "mushrooms"], containsNuts: false },
  { name: "Blue Moon", ingredients: ["blue cheese", "garlic", "walnuts"], containsNuts: true },
  { name: "Taste Of Athens", ingredients: ["spinach", "kalamata olives", "sesame seeds"], containsNuts: true }
];
```

위의 데이터를 참고하여,
products[0]['ingredients'] 이럭식의 코드를 reduce로 표현해 보고 싶어 아래와 같이 코드를 짜보았다.

```js
products.reduce(function(acc, cur) {
  return acc['ingredients'];
})
```

그런데..!
" Cannot read property 'ingredients' " 라는 에러가 발생하였고..

이유를 모르겠어서 질문글을 남겼고 친절한 답변을 통해 확실하게 reduce에 대해 이해하게 되었다.

console.log의 중요성도 깨달았다. <br>
console.log를 통해 두번째 loop에서 에러가 나는 것을 확인할 수 있다.

```js
products.reduce(function(acc, cur) {
  console.log(acc['ingredients'])
})

// (3) ["artichoke", "sundried tomatoes", "mushrooms"]
// TypeError: Cannot read property 'ingredients' of undefined
```

### 정리
  1. accumulator는 콜백의 반환값을 누적한다.
    - 위의 코드에서 첫번째 콜백의 반환값으로 acc['ingredients']이 acc가 됨.
    - acc = acc['ingredients']
      - acc['ingredients']의 값은 ["artichoke", "sundried tomatoes", "mushrooms"]
    - 두번째로 함수를 돌아줄땐 acc['ingredients']['ingredients'] 이런 상태가 되는데, acc['ingredients']에는 ingredients라는 key가 없기 때문에 " Cannot read property 'ingredients' "라는 에러가 발생했던 것이였다..!

### 수정한 코드

```js
products.reduce(function(acc, cur) {
  return acc.concat(cur['ingredients']);
}, [])
// ["artichoke", "sundried tomatoes", "mushrooms", "roma", "sundried tomatoes", "goats cheese", "rosemary", "black beans", "jalapenos", "mushrooms", "blue cheese", "garlic", "walnuts", "spinach", "kalamata olives", "sesame seeds"]
```
 
 
 [help desk 게시글](https://github.com/yoonhe/TIL/issues/1)


