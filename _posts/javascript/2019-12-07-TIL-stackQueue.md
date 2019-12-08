---
title: "Queue & Stack"
categories:
  - DataStructure
---

## Queue
Queue는 편의점이나 마트에서 물건을 팔때 먼저 들어온 물건을 앞에 진열하여 팔리게하는 것과 비슷하다

![image.png](https://images.velog.io/post-images/yhe228/951a1250-18c1-11ea-af62-df20a61bae43/image.png)

- FIFO(First In First Out), 먼저 집어넣은 데이터가 먼저 나온다.

### 🏃🏻‍♂️ method
1. enqueue
	- 데이터를 집어넣는 메소드(맨 앞 요소) 

2. dequeue
	- 데이터를 추출하는 메소드

### ✍ pseudo code (의사 코드)로 표현
![image.png](https://images.velog.io/post-images/yhe228/bd8cf9b0-18ed-11ea-9380-57e25cc0c460/image.png)
1. 데이터를 담을 공간을 만든다 => {}
2. 초기 index를 0으로 지정해준다.
3. 공간의 형태는 index : value
4. 데이터를 넣는다 - enqueue
    - 값을 추가하고
    - index ++
5. 데이터를 제거한다 - dequeue
    - 값을 제거하고
    - index --
    - 값이 0부터 시작하도록 당겨준다


## Stack
![image.png](https://images.velog.io/post-images/yhe228/00c9d210-18c2-11ea-b433-d50f23f0e41b/image.png)

- LIFO(Last In First Out), 나중에 집어넣은 데이터가 먼저 나옵니다

### 🏃🏻‍♂️ method
1. pop
	- 데이터를 추출하는 메소드(마지막 요소)
2. push
	- 데이터를 집어넣는 메소드
3. peek
	- 스택의 맨 마지막 요소를 제거하지 않고 반환해 주는 메소드
4. empty
	상황에따라 true 또는 false 반환
	- 스택이 비어 있으면 true
    - 그렇지 않으면 false
5. size
	- 담긴 데이터의 length를 구하기 위한 메소드

### ✍ pseudo code (의사 코드)로 표현
![image.png](https://images.velog.io/post-images/yhe228/cfcb3ba0-18ed-11ea-9380-57e25cc0c460/image.png)
1. 데이터를 담을 공간을 만든다 => {}
2. 초기 index를 0으로 지정해준다.
3. 공간의 형태는 index : value
4. 데이터를 넣는다 - push
    - 값을 추가하고
    - index ++
5. 데이터를 제거한다 - pop
    - 값을 제거하고
    - index --
6. 공간의 index - 1 번째에 있는 값을 반환 - peek
7. 공간의 index가 0이면 false 0이 아니면 true를 반환 - empty
8. 공간의 index 반환 - size
    

💁‍♀️ [참고블로그](https://medium.com/@lyhlg0201/immersive-sprint-js-stack-queue-426ccfbdb602)




