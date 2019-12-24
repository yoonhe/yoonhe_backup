---
title: "Checkpoints 10 - 8 문제 해결 TIL"
categories:
  - Im_Flex
---

8번 - After the following code runs, what will be the value of result?

```js
var x = 10;

var obj = {
  y: x,
  z: obj.y + 1
};

var result = obj.z;
```

나는 처음에 위의 코드에서 에러가 나는 이유가 객체는 자신의 key, value를 참조할 수 없기때문에 `z: obj.y + 1`에서 에러가 난다고 생각했다.  
확실한 이해를 위해 help desk에 질문을 올렸고 내가 잘못 이해하고 있었다는 사실을 알게되었다😂

obj.z의 value로서 `obj.y`가 참조되는 시점에서 obj가 정의된 상태가 아니기때문에 에러가 났던 것이였다..  

```js
var x = 10;

var obj = {
  y: x
};
obj.z = obj.y + 1
obj // {y: 10, z: 11}
```

obj를 정의해주고 obj.z의 value로 `obj.y`를 참조하면 에러가 발생하지 않고 잘 실행된다.  

잘못이해하고 넘길뻔 했던 문제를 확실하게 짚고 넘어가서 정말 다행이다.
