---
title: "Nodejs & Testing & Linting"
categories:
  - Im_Flex
---

## 1. Node.js 설치하는 방법 

### < MacOS/Linux(ubuntu) >

1. Install NVM  

    아래 명령어 터미널에 입력

    ```
    $ touch ~/.bash_profile 
    $ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.1/install.sh | bash
    ```

2. 버전이 잘 나오면 NVM 설치 성공!

    ```
    $ nvm --version
    ```

3. Install Node

    NVM을 사용하여 Node.js를 설치  

    아래 명령어와 같이 설치하고싶은 node version을 입력해준다

    ```
    $ nvm install 10.13.0
    ```

4. Node 버전이 확인된다면 Node 설치 성공!

    ```
    $ node -v
    ```

### < Window에서 설치하는 방법 >
... 작성중 ...


## 2. Jest 설치방법
- jest는 우리가 작성한 코드가 의도대로 작동하는지, 코드에 결함이나 문제가 없는지 테스트해주는 테스팅 툴이다.

Install NVM 터미널에 아래의 코드 입력

```
npm install --save-dev jest
```

테스트 함수 작성

```js
// sum.js
function sum(a, b) {
  return a + b;
}

module.exports = sum;
```

테스트 함수가 여러개일 때

```js
module.exports = {
  add,
  substract,
  multiply,
  divide,
  describe
};
```

테스트 코드 작성

```js
const sum = require('./sum');

test('adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3);
});
```

테스트 코드가 여러개 일 때

```js
const { add, substract, multiply, divide, describe} = require("../math");
```
  
여러개의 테스트 코드를 그룹으로 묶을 수 있다.

```js
  describe('<math test>', () => {
    test('adds 1 + 2 to equal 3', () => {
      expect(add(1, 2)).toBe(3);
    });

    test('substract 4 - 2 to equal 2', () => {
      expect(substract(4, 2)).toBe(2);
    });
  });
```

이렇게 하면 터미널에 그룹핑되어 보여진다!  

![image.png](https://images.velog.io/post-images/yhe228/10378120-13db-11ea-8094-63df714e4217/image.png)


## 02. ESlint 설치방법

ESLint는 코드규칙을 정해 일관된 코드스타일을 유지해 코드 파악을 용이하게 해주고 오류를 쉽게 찾을 수 있도록 도와주는 툴이다.

터미널에 설치 코드 입력

```
npm install eslint --save-dev
```

구성 파일 설정 코드 입력

```
$ npx eslint --init
```
  
위의 코드를 입력하면 여러가지 질문을 받게되는데 본인의 프로젝트 성향에 맞춰 선택하면 된다.  
그리고 질문중에 인기있는 스타일을 추천해주는 질문이 있는데 그때 airbnb를 선택하면 airbnb의 스타일 가이드와 동일하게 '.eslintrc.json' 코드를 구성해 준다.

### ESLink를 적용하여 코드를 작성해 본 후 느낀점

1. 세미콜론을 찍는 습관
2. 들여쓰기 습관
3. 일관성 있는 스페이스바 사용
4. 가독성 좋은 코드



 



