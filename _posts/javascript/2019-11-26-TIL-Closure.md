---
title: "Closure"
categories:
  - JavaScript
---

## 클로저 : 외부 함수의 변수에 접근할 수 있는 내부 함수

```js
function outerFn() {
  let outerVar = 'outer';
  console.log(outerVar);

  function innerFn() { // 클로저 함수
    let innerVar = 'inner';
    console.log(innerVar);
  }

  return innerFn;
}

let globalVar = 'golbal';
let innerFn = outerFn();
innerFn();
```

### 클로저 함수 안에서는 아래의 3가지에 모두 접근 가능합니다

- 지역 변수(innerVar)
- 외부 함수의 변수(outerVar)
- 전역 변수(globalVar)


### 유용한 클로저 예제

1. 커링
  - 함수 하나가 n개의 인자를 받는 대신, n개의 함수를 만들어 각각 인자를 받게 하는 방법

    ```js
    function adder(x) {
      return function(y) {
        return x + y;
      }
    }
  
    adder(10)(20); // 30
  
    let add100 = adder(100); // x의 값을 고정해놓고 재사용할 수 있다
    add100(2) // 102
    ```
  
2. 템플릿 함수
  - 외부 함수의 변수가 저장되어 마치 템플릿 함수와 같이 사용 가능

    ```js
    function htmlMaker(tag) {
      let startTag = '<' + tag + '>';
      let endTag = '</' + tag + '>';
  
      return function(content) {
        return startTag + content + endTag;
      }
    }
    
    let divMaker = htmlMaker('div');
    
    divMaker('code'); // "<div>code</div>"
    divMaker('states') // "<div>states</div>"
    ```

3. 클로저 모듈 패턴
  - 변수를 스코프 안쪽에 가두어 함수 밖으로 노출 시키지 않는 방법
  - 두 카운터에 각기 다른 count를 다루면서, count를 밖으로 노출시키지 않는다.

    ```js
    function makeCounter() {
      let count = 0;
      return {
        plus : function() {
          count++;
        },
        minus : function() {
          count--;
        },
        getValue : function() {
          return count;
        }
      }
    }
    let count1 = makeCounter();
    count1.plus();
    count1.getValue(); // 1

    let count2 = makeCounter();
    count2.plus();
    count2.plus();
    count2.getValue(); // 2
    ```