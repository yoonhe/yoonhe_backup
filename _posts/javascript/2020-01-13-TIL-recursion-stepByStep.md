---
title: "recursion step-by-step"
categories:
  - JavaScript
---

함수를 호출하면 stack에 execution context(실행 컨텍스트)가 배치된다.

-  stack?
	- stack의 마지막 항목에서 추가와 제거가 발생되는 구조이다.(후입선출)
-  execution contexts(실행 컨텍스트)?
	- 어떤 함수가 호출되면, 실행 컨텍스트 execution context가 만들어진다
    	- call stack에 push
        - 함수를 벗어나면(실행이 끝나면) call stack에서 pop
    - scope 별로 생성된다		
    - 실행 컨텍스트에 담긴것?
      1. 전달 인자
      2. scope 내 변수 및 함수(Local, Global)
      3. 함수 선언 👉🏻 호출된 근원(caller)
      4. this
      
재귀에서 stack에 배치된 실행 컨텍스트는 다른 실행 컨텍스트에서 오는 반환 값을 기다리고 있다. __스택의 마지막 항목이 실행을 마치면 해당 컨텍스트는 반환 값을 생성한다. 이 반환 값은 다음 실행 컨텍스트에 반환 값으로 전달된다.__ 그런 다음 해당 실행 컨텍스트는 스택에서 제거된다.


## 재귀란 ?
- '기본 조건'이 true가 되고 실행이 중지 될 때까지 자신을 호출하는 함수이다.
- 해(solution)가 같은 문제의 조금 더 작은 문제의 해에 의존한다.
- 반복문으로 풀 수 있는 문제는 recursion으로도 풀 수 있다

### 재귀 함수의 구성
1. base cases
	- 뻔한 해가 나오는 경우
    - 종료 조건(terminating case)라고도 불린다
2. recursive cases
	- 문제를 더 작은 문제로 바꿔 자기 자신을 다시 부르는 경우

### 재귀 Case
1. 복잡한 input을 더 간단한 것으로 쪼개어 간다
	- 각 호출마다 input이 점점 base case로 반드시 도달하는 방향으로 쪼개야 한다!

### factorial 예시
- 첫번째 조건 : 매개 변수가 0 또는 1이면 종료하고 1을 반환한다
- 두번째 조건 : 매개 변수가 0 또는 1이 아닌 경우, num-1를 인자로 함수를 다시 호출 한다.

```js
const factorial = function(num) {
  debugger;
  if (num === 0 || num === 1) { // base case
    return 1;
  } else {
    return num * factorial(num - 1); // recursive case
  }
};

factorial(5);
```

1. 실행 스택의 첫번째에 인자로 `5`를 사용하는 factorial()이 배치된다. base case가 false 이므로 다시 재귀 함수를 실행한다.
2. 실행 스택의 두번째에 인자로 `num-1(5-1) = 4`를 사용하는 factorial()이 배치된다. base case가 false이므로 다시 재귀 함수를 실행한다.
3. 실행 스택의 세번째에 인자로 `num-1(4–1) = 3`를 사용하는 factorial()이 배치된다. base case가 false 이므로 다시 재귀 함수를 실행한다.
4. 실행 스택의 네번째에 인자로 `num-1(3–1) = 2`를 사용하는 factorial()이 배치된다. base case가 false이므로 다시 재귀 함수를 실행한다.
5. 실행 스택의 다섯번째에 인자로 `num-1(2–1) = 1`를 사용하는 factorial()이 배치된다. base case가 true 이므로 1을 반환한다.

- __스택의 마지막 항목이 실행을 마치면 해당 컨텍스트가 반환 값을 생성한다. 이 반환 값은 재귀 사례에서 다음 항목으로 반환 값이 전달됩니다.__

6. 마지막 실행 컨텍스트에서 num === 1이였기 때문에, 반환값은 1이다. 반환값은 다음 실행 컨텍스트에 전달된다.
7. 다음으로 num === 2, 반환 값은 2 (1 × 2)이다.
8. 다음으로 num === 3, 반환 값은 6 (1 × 2 × 3)이다.
- 지금까지 1 × 2 × 3이다.
9. 다음으로 num === 4(1 × 2 × 3 × 4), 반환값은 24이다.
10. 마지막으로, num === 5(1 × 2 × 3 × 4 × 5)이며 최종 값은 120입니다.

아래의 그림에 표현이 잘 되어있어서 가져왔다. Good ~ 👍👍👍
![image.png](https://images.velog.io/post-images/yhe228/4aff81b0-35d0-11ea-8360-dbbd50d3cf0d/image.png)
이미지 출처 : [freeCodeCamp](https://www.freecodecamp.org/news/recursion-is-not-hard-858a48830d83/)

재귀는 매우 깔끔하다.
	
for 또는 while 루프를 사용하여 동일한 작업을 수행 할 수 있다. 그러나 재귀를 사용하면 더 읽기 쉬운 우아한 솔루션을 얻을 수 있기 때문에 우리는 재귀 솔루션을 사용한다.  
여러 번 작은 문제로 분류 된 문제가 더 효율적이다. 문제를 더 작은 부분으로 나누면 문제를 극복하는 데 도움이된다. 따라서 재귀는 문제를 해결하기위한 분할 및 정복 방식이다.  

- 하위 문제(sub-problems)는 원래 문제보다 해결하기 쉽다.
- 하위 문제(sub-problems)에 대한 솔루션이 결합되어 원래 문제를 해결한다.


## 재귀 활용 예시들

### Fibonacci

```js
const fibonacci = function(num) {
  if (num <= 1) {
    return num;
  } else {
    return fibonacci(num - 1) + fibonacci(num - 2);
  }
};
fibonacci(5);
```

### Recursive arrays

```js
function flatten(arr) {
  let result = [];
  arr.forEach(elem => {
    if (!Array.isArray(elem)) {
      result.push(elem);
    } else {
      result = result.concat(flatten(elem));
    }
  });
  return result;
}
flatten([1, [2], [3, [[4]]]]);
```

### Reversing a string

```js
function reverse(str) {
  if (str.length === 0) {
    return "";
  }
  return str[str.length - 1] + reverse(str.substr(0, str.length - 1));
  // str의 마지막 문자 + reverse(str의 마지막을 제외한 문자)
}

reverse('banna'); // annab
```

### index search

```js
function searchArraySequentially(array, i, j, x) {
  if (i <= j) {
    if (array[i] === x) { // base case
      return i;
    } else { // recursive case
      return searchArraySequentially(array, i + 1, j, x);
    }
  } else { // base case
    return -1;
  }
}
 
var array = ['a', 'b', 'c', 'd', 'e'];
var result1 = searchArraySequentially(array, 0, 4, 'e');
var result2 = searchArraySequentially(array, 0, 3, 'e');
console.log(result1); // 4;
console.log(result2); // -1;
```

### 👨‍🏫 [참고 블로그]([참고블로그](https://www.freecodecamp.org/news/recursion-is-not-hard-858a48830d83/))
