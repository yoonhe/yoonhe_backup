---
title: "알고리즘 문제를 어떻게 풀어나갈까?"
categories:
  - JavaScript
---

## 알고리즘은 어떠한 문제를 해결하기 위한 절차를 만들어 내는 과정, 혹은 형태이다.

1. 문제를 찾로 큰 문제를 잘게 분해한다
2. 절차를 추론한다
3. 반복되는 패턴을 찾는다


## 문제를 풀기 전에, 과정을 하나하나 pseudocode (의사코드)로 적어낼 수 있다.

1. 프로그램의 절차 하나하나를 우리가 실제로 사용하는 일반적인 언어을 이용해서 작성하는 방법
2. 이는 실제로 컴퓨터가 알아들을 수 있는 언어가 아니기 때문에 실행할 수 있는 코드는 아니지만 코딩하기 전에 어떻게 프로그램이 작동하는지 흐름을 파악할 수 있다

## 알고리즘 예제

- 텍스트에서 foo라는 단어를 찾아 전부 다른 단어로 바꿔주는 코드작성

### 01. pseudocode 작성

1. 텍스트를 입력으로 받는다
  - foo라는 단어를 찾는다
    * foo라는 글자의 index가 -1이 아니면 단어를 찾은 것이다
  - 단어를 발견하면
    1. index를 이용해 foo 바로 앞까지의 텍스트를 얻어낸다.
    2. foo 대신 새로운 단어를 넣는다
    3.  foo 이후의 텍스트를 넣는다 

2. 바뀐 내용을 리턴한다

```js
function find(text, searchString) {
  // foo라는 글자의 index가 -1이 아니면 단어를 찾은 것이다
  return text.indexOf(searchString);
}

function replace(text, searchString, replaceString) {
    let index = find(text, searchString);
    console.log(index);
     let beforeText = text.slice(0, index); // index를 이용해 foo 바로 앞까지의 텍스트를 얻어내고
     let replaceTest = replaceString; // foo 대신 새로운 단어를 넣는다
     let afterTest = text.slice(index + searchString.length); // foo 이후의 텍스트를 넣는다
     
     if(index !== -1) { // index를 발견하면
       return beforeText + replaceTest + afterTest; // 바뀐 내용을 리턴한다
     }
}

find('abcfoodef', 'foo', 'yoon')
```

## 배운것

1. 문제를 풀기전 pseudocode(의사코드) 사용의 중요성
2. function을 통해 기능을 분리하는 방법
