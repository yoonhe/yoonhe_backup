---
title: "Toy Problem 1번 - rockPaperScissors"
categories:
  - algorithm
---

가위바위보의 경우의 수를 구하는 문제에 도대체 어떻게 접근해야할지 감이 안잡혀
help desk에 물어본 결과 아래와 같은 좋은 답변을 받을 수 있었다..!

![image.png](https://images.velog.io/post-images/yhe228/deab6720-2140-11ea-9c2e-09a6267319ca/image.png)

그래서, 엔지니어분의 말씀 처럼 rockPaperScissors(0), rockPaperScissors(1), rockPaperScissors(2), rockPaperScissors(3)의 결과를 직접 써보면서 규칙을 찾기 시작했다.  
정말로 말씀하신대로 나열된 전체 결과를 눈으로 확인해보니 손도 못대는 정도에서는 벗어날 수 있었다..!! 
```
rockPaperScissors(0) = [[], [], []]
rockPaperScissors(1) = [ [ 'rock' ], [ 'paper' ], [ 'scissors' ] ]
rockPaperScissors(2) = [ [ 'rock', 'rock' ],
                        [ 'rock', 'paper' ],
                        [ 'rock', 'scissors' ],
                        [ 'paper', 'rock' ],
                        [ 'paper', 'paper' ],
                        [ 'paper', 'scissors' ],
                        [ 'scissors', 'rock' ],
                        [ 'scissors', 'paper' ],
                        [ 'scissors', 'scissors' ] ]
* rockPaperScissors(3) = 
[["rock","rock","rock"],["rock","rock","paper"],
["rock","rock","scissors"],["rock","paper","rock"],
["rock","paper","paper"],["rock","paper","scissors"],
["rock","scissors","rock"],["rock","scissors","paper"],
["rock","scissors","scissors"],["paper","rock","rock"],
["paper","rock","paper"],["paper","rock","scissors"],
["paper","paper","rock"],["paper","paper","paper"],
["paper","paper","scissors"],["paper","scissors","rock"],
["paper","scissors","paper"],["paper","scissors","scissors"],
["scissors","rock","rock"],["scissors","rock","paper"],
["scissors","rock","scissors"],["scissors","paper","rock"],
["scissors","paper","paper"],["scissors","paper","scissors"],
["scissors","scissors","rock"],["scissors","scissors","paper"],
["scissors","scissors","scissors"]]
   */
```

### 찾은 규칙
바로 전 결과값 배열을 순회하여 각각의 요소에 접근한 뒤 접근한 요소에 "rock", "paper", "scissors"를 각각 하나씩 연결시켜 새로운 배열을 만들어 새로운 공간에 넣어준다.
바로 전 결과값은 순회용으로만 사용하고 현재 결과값은 새로운 공간에 만들어줘야 한다.
예시) 
rockPaperScissors(1)일때 => [ 'rock']
rockPaperScissors(2)일때 => [ 'rock', 'rock' ], [ 'rock', 'paper' ], [ 'rock', 'scissors' ]
rockPaperScissors(3)일때 => [ 'rock', 'rock', 'rock'], [ 'rock', 'rock', 'paper'], [ 'rock', 'rock', 'scissors']

이렇게 숫자가 늘어날때마다 각 요소에 rock, paper, scissors가 붙어서 3배로 늘어난다.

## 풀이 순서
0. rock, scissors, paper를 담을 공간을 만든다(배열) => let storage;
1. 0일땐 별다른 규칙이 없어보이므로 다음 1을 위해 결과값을 담는 공간(storage)에 빈배열 3개를 push해준다. => [[], [], []]
2. 1일때도 2,3...과 같은 규칙이 없어보이므로 0에서 만들어준 각각의 빈배열에 rock, scissors, paper를 push해준다. => [['rock'], ['sissors'], ['paper']]
3. 2부터는 공통 규칙이 보인다.
	1. 결과값을 담는 공간(storage)을 순회하여 각 요소에 접근한다.
    2. 각 요소에 접근한뒤 rock, scissors, paper가 담긴 base를 각각 순회하여 현재 접근한 storage 요소에 연결시켜 새로운 저장공간에 push해 준다. 이과정을 result의 각각의 요소에서 반복한다. => concat 사용
    	- ex) 2일때, ['rock','rock'], ['rock','scissors'], ['rock','paper'].....
        - 새로운 저장공간을 만들어주는 이유?
        	- 앞에서 만들어진 결과값과 겹치면 값이 달라지기 때문에 새로운 저장공간에 현재 결과값을 담아 준 후 마지막에 result에 다시 할당해주기 위해서.

## 코드
```js
var rockPaperScissors = function(number) {
  let basic = ["rock", "paper", "scissors"];
  let storage = [];

  if (number === undefined) {
    number = 3;
  }

  let check = function(count) {
    let newStorage = [];
    if (count === 0) {
      basic.forEach(elem => storage.push([]));
    } else if (count === 1) {
      storage.forEach((elem, idx) => elem.push(basic[idx]));
    } else {
        storage.forEach(elem => {
        basic.forEach(item => newStorage.push(elem.concat(item)));
        storage = newStorage;
      });
    }

    if (number === count) {
      return;
    }

    check(count + 1);
  };

  check(0);

  return storage;
};
```



### 👨‍🏫 reference
```js
var rockPaperScissors = function(rounds) {
  var sequences = [];
  var plays = ['rock', 'paper', 'scissors'];

  var generate = function(sequence, round) {
    // Base case:
    if (round === rounds) {
      sequences.push(sequence);
    } else {
      plays.forEach(function(play) {
        generate(sequence.concat(play), round + 1);
      });
    }
  };

  generate([], 0);
  return sequences;
};
```
0일때 => ` [[]] `
1일때 => `[['rock'], ['paper'], ['scissors']]`
2일때 => `[['rock', 'rock'], ['rock', 'paper'], ['rock', 'scissors'], ['paper', 'rock'], ['paper', 'paper'], ['paper', 'scissors'], ['scissors', 'rock'], ['scissors', 'paper'], ['scissors', 'scissors'] ]`

#### ex) 숫자가 3일때
1. `[]` 빈배열부터 시작한다. 숫자 : 0
2.  var plays = ['rock', 'paper', 'scissors']의 각요소를 순회한다.
3. 첫번째로 'rock'요소에 접근한 후 1번의 `[]`에 연결시켜준 후 그것을 재귀함수의 첫번째 인자로 넣고 두번째 인자인 숫자에 +1을 하여 재귀함수를 실행한다.
4. 두번째 인자의 숫자(1)와 목표숫자인 3이 같지 않으므로 다시 play의 각 요소를 순회한다.
5. 첫번째로 'rock' 요소에 접근한다. 그릴고 현재 첫번째 인자로 들어온 ['rock']에 연결시켜준다. 그리고 그것을 재귀함수의 첫번째 인자로 넣고, 두번째 인자 숫자에 + 1을 해주고 재귀함수를 실행한다.
6. 현재 인자로 넘어온 숫자와 목표 숫자가 같지 않으므로 위의 과정을 목표 숫자가 같을때 까지 반복해준다.
7. 현재 인자로 넘어온 숫자와 목표 숫자가 같다면 sequences 배열에 push해 준다.
8. 이렇게 plays의 각 요소에 재귀함수를 실행시켜주면서 목표숫자와 같아지면 결과값에 push해주고 한 요소 안에서 재귀가 끝나면 그 다음 요소에 재귀를 실행하는 식으로 진행하면 된다.

## 느낀점
역식 reference 코드는 이해가 쉽고 가독성이 좋다. 코드를 읽다보니 rockPaperScissors의 규칙이 눈에 보였다.
내 코드도 이해쉽고 가독성 좋은 코드가 되는 날이 오기를 바라며 비교 분석 열심히 해보았다.
