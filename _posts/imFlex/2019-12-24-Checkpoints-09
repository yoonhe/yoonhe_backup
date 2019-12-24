title: "Checkpoints 09 TIL"
categories:
  - Im_Flex
---

💁‍♀️ 오늘 알게된 사실  
- 객체에 새로운 값을 설정해 주면 현재 참조하고 있던 주소값은 제거되고 다른 reference type을 가리키게 된다.

### 3번 - After the following code runs, what will be the value of x.foo?
👉🏻 x.foo === 3

```js
var x = { foo: 3 };
var y = x;
y = 2;
```

### 4번 - After the following code runs, what will be the value of myArray?
👉🏻 myArray === [2, 3, 4, 5]

```js
var myArray = [2, 3, 4, 5];
var ourArray = myArray;
ourArray = [];
```

### 5번 - After the following code runs, what will be the value of myArray?
👉🏻 myArray === [2, 3, 4, 5]

```js
var myArray = [2, 3, 25, 5];
var ourArray = myArray;
ourArray[2] = 25;
ourArray = undefined;
```

### 7번 - After the following code runs, what will be the value of myArray?
👉🏻 myArray === [2, 3, 4, 5]

```js
var myArray = [2, 3, 4, 5];
function doStuff(arr) {
  arr = [];
}

doStuff(myArray);
```

### 8번 - After the following code runs, what will be the value of player.score?
👉🏻 player.score === 2

```js
var player = { score: 3 };
function doStuff(obj) {
  obj.score = 2;
  obj = undefined;
}

doStuff(player);
```

### 9번 - After the following code runs, what will be the value of player?
👉🏻 player === undefined

```js
var player = { score: 3 };

function doStuff(obj) {
  obj = {};
}

player = doStuff(player);
```
