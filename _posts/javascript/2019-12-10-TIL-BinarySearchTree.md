---
title: "Data structure - Binary Search Tree"
categories:
  - DataStructure
---

## 이진탐색트리(Binary Search Tree)

- 이진탐색트리란 이진탐색과 연결리스트(Linked list)를 결합한 자료구조의 일종이다.
- 이진탐색의 효율적인 탐색 능력 + 연결리스트의 효율적인 자료 입력과 삭제 기능
- 이진탐색과 연결리스트가 서로의 단점을 보완해준다.
![image.png](https://images.velog.io/post-images/yhe228/2d9a0ba0-1b08-11ea-af97-59e7d03a8f7d/image.png)

### 이진탐색트리 동작 원리
- 왼쪽 서브트리는 루트노드보다 작은 값을 가진 노드로 이루어져 있다.
- 오른쪽 서브트리는 루트노드보다 큰 값을 가진 노드로 이루어져 있다.
- 왼쪽과 오른쪽 서브트리도 이진탐색트리이다.
- 중복된 노드가 없어야 한다.


![image.png](https://images.velog.io/post-images/yhe228/07fceaa0-1b0a-11ea-b4c8-d5ec753f7f37/image.png)
위와 같은 트리에서 `11`을 탐색한다고 가정했을때,  
1. 루트노드(8)가 `11`보다 작기때문에 왼쪽 서브트리는 탐색할 필요가 없으며 오른쪽 서브티리만 탐색하면 된다. 탐색공간이 줄어들었다..!
2. 서브트리의 루트노트(9)가 `11`보다 작기때문에 오른쪽 서브트리를 탐색한다.
3. 오른쪽 트리에 있는 11을 찾았다.



💁‍♀️ [참고블로그](https://ratsgo.github.io/data%20structure&algorithm/2017/10/22/bst/)
