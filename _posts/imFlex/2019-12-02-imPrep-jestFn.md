---
title: "jest.fn()"
categories:
  - Im_Flex
---

## jest.fn()

jest는 mock 기능을 지원한다.  

1. mocking이란?
  - 단위 테스트를 작성할 때, 해당 코드가 의존하는 부분을 가짜(mock)로 대체하는 기법이다.
  - mocking은 이러한 상황에서 실제 객체인 척하는 가짜 객체를 생성하는 매커니즘을 제공
  - 테스트가 실행되는 동안 가짜 객체에 어떤 일들이 발생했는지를 기억하기 때문에 가짜 객체가 내부적으로 어떻게 사용되는지 검증할 수 있다.
  - mocking을 이용하면 실제 객체를 사용하는 것보다 훨씬 가볍고 빠르게 실행되면서도, 항상 동일한 결과를 내는 테스트를 작성할 수 있다.


Jset는 가짜 함수(mock functiton)를 생성할 수 있도록 jest.fn() 함수를 제공한다.

```js
const mockFn = jest.fn();
```

가짜 함수는 자신이 어떻게 호출되었는지를 모두 기억한다.  
그래서 테스트를 작성할 때 가짜 함수가 유용하다..!

```js
mockFn('a');
mockFn(['b', 'c']);

expect(mockFn).toBeCalledTimes(2);
expect(mockFn).toBeCalledWith('a');
expect(mockFn).toBeCalledWith(['b', 'c']);
```

[참고 사이트 링크](https://www.daleseo.com/jest-fn-spy-on/)


