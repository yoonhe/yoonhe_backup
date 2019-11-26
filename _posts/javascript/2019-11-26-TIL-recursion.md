---
title: "Recursion"
categories:
  - JavaScript
---

## Recursion

Recursion은 Function이 스스로를 내부에서 부르게 하여 문제를 해결하는 기술이다. 이렇게 하면 소량의 처리만 완료하고 나머지 문제를 재귀 호출에 위임할 수 있다.

- 함수를 스스로 호출하는 것
- 재귀는 반복할 구문을 함수 단위로 분리해, 특정 조건이 만족할 때 까지 실행하는 패턴으로 볼 수 있습니다.
- 재귀는 무한 반복을 방지하기 위해 탈출 조건이 있어야 합니다.

### 재귀 무한루프

```js
function foo() {
  foo()
}
```

![image.png](https://images.velog.io/post-images/yhe228/52e73b90-e416-11e9-855b-c9c70516744a/image.png)  

  - < Uncaught RangeError: Maximum call stack size exceeded > 
    * call stack에 더이상 담을 수가 없다는 에러
   
### call stack?

1. 어떤 함수가 호출되면, 실행 컨텍스트 execution context가 만들어진다.
2. call stack에 push
3. 함수를 벗어나면 call stack에서 pop 
4. 함수 실행시 callstack이 해소되는 과정
  - 자바스크립트는 함수를 스택 위에 올리고 함수가 실행되고 끝이 나면 pop하여 없애는 것을 확인할 수 있었다.
    * [참고링크](https://shlee0882.tistory.com/212)

![image.png](https://images.velog.io/post-images/yhe228/bfceb800-e416-11e9-8a8d-f7ea9a766832/image.png)

### 탈출 조건이 있는 재귀 예시

```js
function eat(food) {
  console.log('먹기 전 음식 리스트 => ', food);
  console.log('지금 먹고있는 음식 ? ', food.pop());
  if(food.length) { // 탈출 조건
    eat(food);
  } else {
    console.log('먹을 음식이 없습니다.')
  }
}
```

-  결과 
  ```js
  eat(['피자','치킨','족발'])
  VM552:2 먹기 전 음식 리스트 =>  (3) ["피자", "치킨", "족발"]
  VM552:3 지금 먹고있는 음식 ?  족발
  VM552:2 먹기 전 음식 리스트 =>  (2) ["피자", "치킨"]
  VM552:3 지금 먹고있는 음식 ?  치킨
  VM552:2 먹기 전 음식 리스트 =>  ["피자"]
  VM552:3 지금 먹고있는 음식 ?  피자
  VM552:7 먹을 음식이 없습니다.
  ```


### 재귀 활용 예시들

- 팩토리얼 함수 

  ```js
  function factorial(n) {
    if (n === 0) {
    return 1;
    }
  
    return n * factorial(n-1);
  }
  factorial(3)
  /*
  factorial(3) ?
  = 3 * factorial(2)
  = 3 * 2 * factorial(1)
  = 3 * 2 * 1 * factorial(0)
  = 3 * 2 * 1 * 1
  = 6
  */
  ```

- fibonacci 수열

  ```js
  function fibonacci(n) {
      if (n < 2)
          return n;
      return fibonacci(n - 1) + fibonacci(n - 2);
  }
  
  /*
  fibonacci(5) ?
  1. fibonacci(4) + fibonacci(3)
    1) fibonacci(4) = fibonacci(3) + fibonacci(2)
      1-1) fibonacci(3) = fibonacci(2) + fibonacci(1)
                        = fibonacci(2) + 1     
                        = ( fibonacci(1) + fibonacci(0) ) + 1
                        = 1 + 1
                        = 2
                        
      1-2) fibonacci(2) = 1
    
    * 1번 결과 fibonacci(4) = 2 + 1 = 3
  
    2) fibonacci(3) = fibonacci(2) + fibonacci(1)
                    = 1 + 1 = 2
  
    * 2번 결과 = 2
    
    1번 + 2번 합은 5
  */
  ```

  - [팩토리얼 함수 참고 링크](https://www.everdevel.com/JavaScript/recursive-function.php)
  - [피보나치 수열 참고 링크 - 1](https://www.codeit.kr/questions/1446)
  - [피보나치 수열 참고 링크 - 1](https://homoefficio.github.io/2015/07/27/%EC%9E%AC%EA%B7%80-%EB%B0%98%EB%B3%B5-Tail-Recursion/)

  
### for문을 재귀로 표현할 수도 있음
  
  - for문

    ```js
    for(let i=0; i<3; i++) {
      console.log('hi)
    }
    ```

  - 재귀

    ```js
    function printHello(count) {
      if(count === 0) {
        return;
      }
      console.log('hi');
      debugger; 
      printHello(count - 1)
    }
  
    printHello(3)
    ```


3. tree 구조 탐색
  - JSON : JavaScript Object Notation
    * 재귀는 트리구조, 탐색기를 다룰때 유용하게 쓰임
  - DOM
    * DOM 탐색에도 유용함.

4. 재귀의 장, 단점
  - 장점 : 알고리즘이 재귀로 표현하기에 자연스러울 경우, 프로그램의 가독성이 좋다.
  - 단점 : 값이 리턴되기 전까지 호출마다 call stack을 새로 생성하므로, 메모리를 많이 사용한다.

### 재귀의 단점 보완

1. 메모이제이션(memoization)
  - memo 배열에 계산한 값을 저장
  - 다시 계산하지 않고 사용하도록 기억시킨다 
  
2. 메모이제이션 예시

  - 피보나치 수열
  
      ```js
      let callCount = 0;
      let fibonacci = (function() {
          let memo = [0,1];
          let fib = function(n) {
            callCount++;
            let result = memo[n];
            if(typeof result !== 'number') {
              // 없으면 계산해서 넣어라
              result = fib(n - 1) + fib(n - 2);
              memo[n] = result;
            }
            // 값이 저장되어있으면 있는거 사용
            return result;
            }
      
          return fib;
      }());
      let result = fibonacci(10);
      console.log('callCount ? ', callCount); // callCount ?  19
      console.log(result); // 55
      ```

  - 팩토리얼
  
      ```js
      let factorial = (function() {
        let save = {};
        let fact = function(number) {
          console.log(save)
          if(number > 0) {
            let saved = save[number - 1] || fact(number - 1);
            let result = number * saved;
            save[number] = result;
            return result;
          } else {
            return 1;
          }
        }
        return fact;
      }) ();
      factorial(3);
      factorial(4); // save = {1: 1, 2: 2, 3: 6}
      factorial(5) // save = {1: 1, 2: 2, 3: 6, 4: 24}
      ```

  - [참고글](https://www.zerocho.com/category/JavaScript/post/579248728241b6f43951af19)



