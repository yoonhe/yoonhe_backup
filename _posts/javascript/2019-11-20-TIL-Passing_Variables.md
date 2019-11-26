---
title: "변수의 전달"
categories:
  - JavaScript
---

## JavaScript에서의 Primitive Types & Reference Types

JavaScript에서 변수의 전달 방법인 pass-by-value, 그리고 또다른 방법인 pass-by-reference에 대한 설명이다.

- JavaScript에는 두가지 종류의 변수 타입이 있다
  * primitive
  * reference
- 변수가 생성되고 난 후, 고정된 크기의 메모리가 예약이 된다.
- 변수를 복사한 후, 고유의 메모리값이 복사된다.
- 호출을 통해 변수를 함수에 전달하면, 해당 변수의 복사본이 생성된다

### 01. Primitive Types (원시 타입)

Primitive type의 메모리상의 값은 그것의 실제 값이다(예를 들어, boolean의 경우 true, number의 경우 42).  
Primitive type은 고정된 크기의 메모리에 저장할 수 있다.

- null
- undefined
- Boolean
- Number
- String

Primitive type은 scalar type 또는 simple type으로도 불린다.

### 02. Reference Types

Reference type은 다른 값을 포함할 수 있다.  
Reference type의 내용은 고정된 크기의 메모리에 저장이 불가능하므로,  
메모리 상에서의 Reference type의 값은 참조 그 자체(메모리 주소)를 담고 있다.

- Array
- Object
- Function

Reference type은 complex type 또는 container type으로도 불린다.  

### 03. 코드 예제

  - Copying a primitive

    ```js
    let a = 13         
    let b = a          
    b = 37             
    console.log(a)     // => 13
    ```
    - 원본은 변하지 않고 복사본만 변했다.

  - Copying a reference
  
    ```js
    let a = { c: 13 }  
    let b = a          
    b.c = 37           
    console.log(a)     // => { c: 37 }
    ```
    - 메모리 주소를 복사했으므로, 원본 역시 변했다.


## 넘기는 변수의 타입이 무엇이냐에 따라 전달의 형태가 달라진다

- 문자열(string), 숫자(number), 불리언(boolean), null, undefined ➡ 값을 복사해서 넘김(pass by value)

  ```js
  let text = 'hello world';
  
  function passByValue(param) {
    param = 'good bye';
  }
  
  passByValue(text);
  console.log(text); // 'hello world'
  ```

- 객체(object), 배열(array), 함수(function) ➡ 참조(주소값)을 복사해서 넘김(pass by reference)

  ```js
  let obj = {greeting : 'hello world'};
  
  function passByReference(param) {
    param.greeting = 'goodbye world';
  }
  
  passByReference(obj);
  
  console.log(obj) // {greeting: "goodbye world"}
  ```

### 배운 내용 확인

```js
let array = ['zero', 'one', 'two', 'three', 'four'];

function passedByReference(refArray) {
  refArray[1] = 'changed in function';
}
passedByReference(array);
console.log(array) // ["zero", "changed in function", "two", "three", "four", "five"]

let assignedArray = array;
assignedArray[5] = 'changed assignedArray';
console.log(array) // ["zero", "changed in function", "two", "three", "four", "changed assignedArray"]

let copyOfArray = array.slice();
copyOfArray[3] = 'changed in copyOfArray';
console.log(array) // ["zero", "changed in function", "two", "three", "four", "changed assignedArray"]
```
