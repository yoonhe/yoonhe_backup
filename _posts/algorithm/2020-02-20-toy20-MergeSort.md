---
title: "Toy problem 20번 - Merge Sort"
categories:
  - algorithm
---

Merge Sort라는 문제는 순서가 뒤죽박죽인 배열을 sort를 사용하지 않고 배열을 오름차순으로 정렬하는 문제인데 어떻게 Sort를 사용하지 않고 오름차순으로 정렬해야할지 감이 잡히지 않아 구글에 검색해보았더니 Merge Sort(병합정렬) 방법에 대한 글이 많이 나왔다. 그 중 그림으로 표현이 잘되어있는 글을 보고 이해한 내용을 정리한다


Merge Sort는 데이터들을 잘게 쪼갠 다음에 하나로 합치는 과정에서 정렬하는 방법이다

```
1. [4,7,4,3,9,1,2] -> [[4],[7],[4],[3],[9],[1],[2]]
2. [[4],[7],[4],[3],[9],[1],[2]] -> [[4,7],[3,4],[1,9],[2]]
3. [[4,7],[3,4],[1,9],[2]] -> [[3,4,4,7], [1,2,9]]
4. [[3,4,4,7], [1,2,9]] -> [[1,2,3,4,4,7,9]]
5. [1,2,3,4,4,7,9]
```

아래의 그림에 잘 나타나있다.  
![](https://images.velog.io/images/yhe228/post/6f5d2a47-b6b5-4bff-8a7f-60a1dd34240e/image.png)  

1. 데이터를 반으로 쪼개는 작업을 데이터가 하나만 남을때까지 반복한다
2. 하나씩 쪼개진 데이터를 정렬하여 다시 그룹화한다


처음에는 어떻게 시작해야할지 감이 안잡혔지만 그림을 보고 이해를 한후 코드작성에 들어가니 감이 안잡히는 상태에서 벗어날 수 있었다.

여기서 그림으로 표현하는 것의 중요성을 다시한번 느끼게 되었다..!

```js
function mergeSort(arr) {
/**
* 1. 배열을 반으로 쪼개는 작업을 배열의 길이가 1이 될때까지 실행한다(재귀)
*    1. 배열의 길이를 2로 나누어 중간값을 구한다
*    2. 중간값을 기준으로 배열을 나눈다
* 2. 배열의 길이가 1이 되면 반으로 쪼개진 두개의 배열을 오름차순으로 정렬하여 다시 합쳐준다. 
*/

  if(arr.length === 1) {
    return arr;
  }

  const middleVal = Math.floor(arr.length/2);
  const leftVal = arr.slice(0,middleVal);
  const rightVal = arr.slice(middleVal);

  return merge(mergeSort(leftVal),mergeSort(rightVal));
}

function merge(left, right) {
/**
* index를 0부터 시작하여 left와 right의 현재 인덱스의 값을 비교하여 더 작은 값을 result에 넣어준다
* 
* 더 작은 값이 있는 배열의 인덱스를 + 1 해준다 => 비교값 변경
* left와 right 둘중에 하나라도 현재 인덱스가 배열의 길이보다 크다면 loop를 돌지않는다
=> 배열의 길이보다 큰 인덱스에 값이 존재하지 않기때문
* 
* while문을 빠져나오면 result의 값과 left, right의 현재 인덱스를 반환해준다
*/

  const mergeResult = [];
  let leftIndex = 0;
  let rightIndex = 0;

  while(leftIndex < left.length && rightIndex < right.length) {
    if(left[leftIndex] < right[rightIndex]) {
      mergeResult.push(left[leftIndex]);
      leftIndex++;
    } else {
      mergeResult.push(right[rightIndex]);
      rightIndex++;
    }
  }

  return [...mergeResult,...left.slice(leftIndex), ...right.slice(rightIndex)];
}
```


## 참고블로그
- [병합 정렬(Merge Sort)과 분할 정복 전략(Divide and Conquer) 개념에 대하여](https://im-developer.tistory.com/134)
- [자바스크립트로 합병정렬 구현 (merge sort in javascript)](https://loving-wright-d0eedb.netlify.com/blog/merge-sort-in-javascript)
- [Merge Sort Algorithm in JavaScript](https://medium.com/javascript-in-plain-english/javascript-merge-sort-3205891ac060)
