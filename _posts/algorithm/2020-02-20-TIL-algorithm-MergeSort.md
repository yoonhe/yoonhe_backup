---
title: "Merge Sort"
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
// 배열을 반으로 나누고, 재귀적으로 병합한다.
function mergeSort(arr) {
  debugger;
  // 재귀함수 탈출조건 단일 요소로 구성된 배열이라면, 리턴
  if (arr.length === 1) {
    return arr;
  }
  
  const middle = Math.floor(arr.length / 2); // 배열의 중간 값
  const left = arr.slice(0, middle); // left side items
  const right = arr.slice(middle); // right side items

  return merge(mergeSort(left), mergeSort(right));
}

// 배열을 비교하고, 연결된 결과를 리턴한다.
function merge(left, right) {
  let result = [];
  let leftIndex = 0;
  let rightIndex = 0;

  // left items와 right items 비교
  while(leftIndex < left.length && rightIndex < right.length) {
    if (left[leftIndex] < right[rightIndex]) {
      result.push(left[leftIndex]);
      leftIndex++;
    } else {
      result.push(right[rightIndex]);
      rightIndex++;
    }
  }

  let outputArr = [...result, ...left.slice(leftIndex), ...right.slice(rightIndex)];
  return outputArr
}

const list = [2, 5, 1, 3, 7, 2, 3, 8, 6, 3];
console.log(mergeSort(list)); // [ 1, 2, 2, 3, 3, 3, 5, 6, 7, 8 ]
```


## 참고블로그
- [병합 정렬(Merge Sort)과 분할 정복 전략(Divide and Conquer) 개념에 대하여](https://im-developer.tistory.com/134)
- [자바스크립트로 합병정렬 구현 (merge sort in javascript)](https://loving-wright-d0eedb.netlify.com/blog/merge-sort-in-javascript)
- [Merge Sort Algorithm in JavaScript](https://medium.com/javascript-in-plain-english/javascript-merge-sort-3205891ac060)
