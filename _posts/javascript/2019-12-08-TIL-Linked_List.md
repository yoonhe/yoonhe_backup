---
title: "Data structure - Linked list"
categories:
  - DataStructure
---

## Linked list
![image.png](https://images.velog.io/post-images/yhe228/892a1010-19bd-11ea-b9e3-059ed5652c45/image.png)
  
- 엘리먼트와 엘리먼트 간의 연결(link)을 이용해서 리스트를 구현한 것
- Head에는 첫번째 노드에 대한 정보가 저장되어있다.
- 각각의 노드에는 노드값과 다음 노드에 대한 정보가 들어있다. 
- 다음 노드에 대한 정보를 가지고있기 때문에 하나의 연결된 값의 모임을 만들 수 있다.

## 🏃🏻‍♂️ Method
### 1. 데이터 첫번째에 추가
![image.png](https://images.velog.io/post-images/yhe228/bf9030c0-19be-11ea-9289-a93f0ff2adc3/image.png)

#### ✍ pseudo code (의사 코드) 
1. 추가할 새로운 노드를 생성한다.
2. 새로운 노드의 다음 노드를 현재 첫번째 노드로 지정한다.
3. Head에 새로운 노드의 정보를 저장한다.

### 2. 데이터 중간에 추가
![image.png](https://images.velog.io/post-images/yhe228/2cca12f0-19bf-11ea-acb7-3b7386d9213f/image.png)
![image.png](https://images.velog.io/post-images/yhe228/49957140-19bf-11ea-b994-61528d9f4539/image.png)

#### ✍ pseudo code (의사 코드)
1. 추가할 노드를 생성한다.
2. 넣을 자리를 정한다.
3. 넣고자 하는 자리의 앞, 뒤 노드에 대한 정보를 저장해둔다
4. 넣고자 하는 자리의 앞에 위치한 노드의 다음 노드를 새로 추가한 노드로 지정한다.
5. 새로 추가한 노드의 다음 노드를 넣고자 하는 자리의 뒤에 위치한 노드로 지정한다.

### 3. 데이터삭제
![image.png](https://images.velog.io/post-images/yhe228/392ece20-19c2-11ea-8cdc-5d3ac9aaf1e0/image.png)

#### ✍ pseudo code (의사 코드)
1. 삭제할 노드를 정한다
2. `삭제할 노드의 앞에 있는 노드`의 다음 노드를 `삭제할 노드 다음에 위치한 노드`로 지정한다.
3. 삭제하려고 했었던 노드를 삭제한다.

### 4. 데이터조회

![image.png](https://images.velog.io/post-images/yhe228/21b3a8b0-19c7-11ea-92f3-7379627d677e/image.png)

#### ✍ pseudo code (의사 코드)
1. count = 0
2. 찾는값과 해당 인덱스의 값이 일치하지 않을때 count에 +1을 해준다
3. 찾는값과 해당 인덱스의 값이 일치하다면 그때는 count를 반환한다!


* Linked list는 추가, 삭제 기능은 매우 빠르지만, 데이터를 조회하는 기능은 Array보다 느리다.

### 💁‍♀️ [참고사이트](https://opentutorials.org/module/1335/8821)

