---
title: "Prototype?"
categories:
  - JavaScript
---

## prototype
자바스크립트에는 Prototype Link 와 Prototype Object라는 것이 존재한다. 그리고 이 둘을 통틀어 Prototype이라고 부른다.

### 1. Prototype Object

객체는 언제나 함수(Function)로 생성된다

```js
// Object, Array 등등은 자바스크립트에서 기본적으로 제공하는 함수이다.

console.log(Object) // ƒ Object() { [native code] }

var obj = new Object();
console.log(obj) // {}

console.log(Array) // ƒ Array() { [native code] }

let arr = new Array(1,2,3)
console.log(arr) // [1, 2, 3]
```

위와 같이 함수가 정의될 때 2가지 일이 동시에 일어난다..!  

1. 해당 함수에 Constructor(생성자) 자격 부여
	- Constructor 자격이 부여되면 new를 통해 객체를 만들어 낼 수 있게 된다. 이것이 함수만 new 키워드를 사용할 수 있는 이유이다.
    
2. 해당 함수의 Prototype Object 생성 및 연결

	👉 함수를 정의하면 함수만 생성되는 것이 아니라 Prototype Object도 같이 생성된다.
    
    ```js
    function Food(name) {
      this.name = name;
    }

	Food.prototype.eat = function() {
      console.log(this.name + '을 먹습니다');
    }
	```
    ![image.png](https://images.velog.io/post-images/yhe228/9e5d1290-18ad-11ea-913b-9154d8e270a5/image.png)
    
    - 생성된 함수는 `prototype`이라는 속성을 통해 `Prototype Object`에 접근할 수 있다. 
    - `Prototype Object`는 일반적인 객체와 같으며 기본적인 속성으로 `constructor`와 `proto`를 가지고 있다.
    - `constructor`는 Prototype Object와 같이 생성되었던 함수를 가리킨다.
	- `proto`는 Prototype Link이다.
    
### 2. Prototype Link

```js
let food1 = new Food('apple');
```

![image.png](https://images.velog.io/post-images/yhe228/e1bc8d50-18b1-11ea-960b-0991973d88dc/image.png)
                 
- `__proto__`속성은 모든 객체가 빠짐없이 가지고 있는 속성이다.
- `__proto__`는 __객체가 생성될 때 조상이었던 함수의 Prototype Object를 가리킨다.__(그래서 Prototype Object의 속성을 참조하는 것이 가능하다)
- food1객체는 Food함수로부터 생성되었으니 Food 함수의 Prototype Object를 가리키고 있는 것
- `food1`객체가 `eat메소드`를 직접 가지고 있지 않기 때문에 `eat메소드`를 찾을 때 까지 상위 프로토타입을 탐색한다. 최상위인 Object의 Prototype Object까지 도달했는데도 못찾았을 경우 undefined를 리턴한다. 이렇게 `__proto__`속성을 통해 상위 프로토타입과 연결되어있는 형태를 프로토타입 체인(Chain)이라고 한다


    
💁‍♀️ [참고블로그](https://medium.com/@bluesh55/javascript-prototype-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-f8e67c286b67)

    


    
