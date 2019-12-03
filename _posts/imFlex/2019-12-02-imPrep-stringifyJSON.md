---
title: "Recursion 연습 - stringifyJSON"
categories:
  - Im_Flex
---

JSON.stringify() 함수를 Recursion을 사용해 직접 작성해보는 시간을 가져보았다.

## stringifyJSON

먼저 JSON.stringify에 넣고 실행하면 어떤 결과값이 나오는지 파악을 해보았다.

```js
let stringifiableObjects = [
  9,
  null,
  true,
  false,
  "Hello world",
  [],
  [8],
  ["hi"],
  [8, "hi"],
  [1, 0, -1, -0.3, 0.3, 1343.32, 3345, 0.00011999999999999999],
  [8, [[], 3, 4]],
  [[[["foo"]]]],
  {},
  { a: "apple" },
  { foo: true, bar: false, baz: null },
  { "boolean, true": true, "boolean, false": false, null: null },
  // basic nesting
  { a: { b: "c" } },
  { a: ["b", "c"] },
  [{ a: "b" }, { c: "d" }],
  { a: [], c: {}, b: true }
];
stringifiableObjects.map(elem => JSON.stringify(elem));

/*  
///// 결과값 ///// 
0: "9"
1: "null"
2: "true"
3: "false"
4: ""Hello world""
5: "[]"
6: "[8]"
7: "["hi"]"
8: "[8,"hi"]"
9: "[1,0,-1,-0.3,0.3,1343.32,3345,0.00011999999999999999]"
10: "[8,[[],3,4]]"
11: "[[[["foo"]]]]"
12: "{}"
13: "{"a":"apple"}"
14: "{"foo":true,"bar":false,"baz":null}"
15: "{"boolean, true":true,"boolean, false":false,"null":null}"
16: "{"a":{"b":"c"}}"
17: "{"a":["b","c"]}"
18: "[{"a":"b"},{"c":"d"}]"
19: "{"a":[],"c":{},"b":true}"
*/
```

```js
let unstringifiableValues = {
    functions: function() {},
    undefined: undefined
  };

JSON.stringify(unstringifiableValues);

/* 
//// 결과값 //// 
"{}"
*/
```

1. number, boolean, null => 문자열로 변환된다
2. string => 'string'
3. array => '['value']' : 배열 안에 요소도 문자열로 변환된다.
4. object => '{'key':'value'}' : 객체 안에 key, value도 문자열로 변환된다.
5. 객체의 value가 'function' 또는 undefined 라면 빈문자열로 변환된다.



### stringifyJSON 함수 작성 완료!

```js
const stringifyJSON = obj => {
  if (typeof obj === 'number' || typeof obj === 'boolean' || obj === null) {
    return String(obj);
  }
  
  if (typeof obj === 'string') {
    return `"${obj}"`;
  }
  
  if (Array.isArray(obj)) {
    let result = [];

    obj.forEach(elem => result.push(stringifyJSON(elem)));

    return `[${result}]`;
  }
  
  if (typeof obj === 'object') {
    let result = '';
    for (let key in obj) {
      if (typeof obj[key] === 'undefined' || typeof obj[key] === 'function') {
      } else {
        result = result + `${stringifyJSON(key)}:${stringifyJSON(obj[key])},`;
      }
    }
    result = result.substring(0, result.length - 1); // {'a': 1,} => ','는 없어야 하기 때문에!
    return `{${result}}`;
  }
};
```





