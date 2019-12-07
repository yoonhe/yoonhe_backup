## Queue
Queue는 편의점이나 마트에서 물건을 팔때 먼저 들어온 물건을 앞에 진열하여 팔리게하는 것과 비슷하다

![image.png](https://images.velog.io/post-images/yhe228/951a1250-18c1-11ea-af62-df20a61bae43/image.png)

- FIFO(First In First Out), 먼저 집어넣은 데이터가 먼저 나온다.

### 🏃🏻‍♂️ method
1. enqueue
	- 데이터를 집어넣는 메소드(맨 앞 요소) 

2. dequeue
	- 데이터를 추출하는 메소드

### pseudo code (의사 코드)로 표현
```
1. 데이터를 담을 공간을 만든다. - storage = {}
2. 초기 index를 0으로 지정해준다.
2. 담을 공간의 key에 index를 넣어주고 value에 넣고자 하는 값을 넣고, index는 +1을 해준다 => enqueue
3. Object의 delete 연산자로 객체 맨 앞의 속성을 제거해주고 저장공간을 for문으로 돌면서 각각의 index에서 -1을 하여 key값을 새로 만들어 값을 넣어주며 재 구성한다.
4. 재구성된 storage의 마지막 값을 제거해주고 그 후 index는 -1을 해준다.

```


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

### pseudo code (의사 코드)로 표현
```
1. 데이터를 담을 공간을 만든다. - storage = {}
2. 초기 index값을 0으로 지정한다.
3. 공간의 key를 0으로하고 value에 원하는 값을 넣어주고 index에 +1을 해준다.
4. 공간의 index에서 -1을 한 index에 위치하는 값을 추출한다 - pop
5. 공간의 index에서 -1을 한 index에 위치하는 값을 반환한다 - peek
6. 공간의 index가 0이면 false 0이 아니면 true를 반환 - empty
7. 공간의 index가 size가 된다.

```
    

💁‍♀️ [참고블로그](https://medium.com/@lyhlg0201/immersive-sprint-js-stack-queue-426ccfbdb602)
