---
title: "Underbar"
categories:
  - Im_Flex
---

## _.reject

```js
// Return all elements of an array that don't pass a truth test.
_.reject = function(collection, test) {
  // TIP: see if you can re-use _.filter() here, without simply
  // copying code in and modifying it
  let filterTrueElem = _.filter(collection, test);
  let result = _.filter(collection, function(num) {
    return filterTrueElem.indexOf(num) === -1;
  })
  return result;
};

_.filter = function(collection, test) {
  let array = [];
  for(let i = 0; i < collection.length; i++) {
    if(test(collection[i])) {
      array.push(collection[i]);
    }
  }
  return array;
};
```
### test 함수를 통과하지 않는 요소들만 필터하는 문제,
1. test 함수를 통과하는 요소들을 _.filter 함수로 1차 필터
2. 원본배열에서 1차 필터된 배열의 요소와 같지 않은 요소들을 2차 필터하여 리턴 



## _.map

```js
_.map = function(collection, iterator) {
  // map() is a useful primitive iteration function that works a lot
  // like each(), but in addition to running the operation on all
  // the members, it also maintains an array of results.
  let result = [];
  for(let i = 0; i < collection.length; i++) {
    result.push(iterator(collection[i]));
  }
};
```
위와 같이 _.map 함수를 작성하였는데,
```js
it("should produce a brand new array instead of modifying the input array", function() {
  var numbers = [1, 2, 3];
  var mappedNumbers = _.map(numbers, function(num) {
    return num;
  });

  expect(mappedNumbers).not.toEqual(numbers);
});
```
원본배열을 건드리지 않고 새로운 배열을 사용해 함수를 작성하였음에도 불구하고 계속 에러가 떠서 help desk 검색을 해보니..
'toEqual'을 'toBe'로 바꾸면 해결되는 문제였다..! 

### 1. solution

- toEqual : 원본배열이 아니어도 속성 값이 같으면 성립
- toBe : 원본배열과 같은 주소를 참조하여야 성립

테스트 함수내의 numbers와 mappedNumbers는 속성 값은 같지만 참조하는 주소가 다르기 때문에 'not.toEqual'이 아닌 'not.toBe'을 사용해야 한다.

👍 [참고글](https://benmccormick.org/2017/08/15/jest-matchers-1/)

## _.memoize

어떻게 해야 함수에 전달된 parameter를 저장하여 다음에 똑같은 parameter가 들어왔을 때 저장된 값을 사용해야 하는지 고민하고 고민하다 어떻게 접근해야할지 모르겠어 구글링을 해본 결과 아래와 같은 방법으로 문제를 해결할 수 있었다.

1. 클로저 함수의 arguments가 'memo' 변수에 저장되어 있지 않다면 새로 실행된 클로저 함수의 값을 저장해준다.
2. 클로저 함수의 arguments가 'memo' 변수에 저장되어 있다면 저장된 값을 사용한다.

```js
_.memoize = function(func) {
  let memo = {};

  return function() {
    if (memo[JSON.stringify(arguments)] === undefined) {
      memo[JSON.stringify(arguments)] = func.apply(this, arguments);
      // apply => 배열로 받은 argument를 인자로 바꿔 넘긴다.
    }
    console.log(memo);
    return memo[JSON.stringify(arguments)];
  };
};
```

이번에는 구글링을 통해 해결했지만, 오늘 알게된 개념을 잘 기억해서 다음에 응용된 문제가 나오더라도 풀 수 있도록 확실하게 짚고 넘어가자!
