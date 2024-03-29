---
title: "Data structure - Tree Map Mathod "
categories:
  - DataStructure
---
## Tree Map Mathod 

Tree의 메소드인 map을 구현하는데 시간이 오래 걸렸다..  
map 메소드는 아래와 같은 특성을 가진다.  
1. 기존 객체와 같은 구조이되 객체의 값들은 callback 함수에 순서대로 넣어 실행시킨 값이어야 한다.
	- 기존 객체의 주소값을 참조하면 안됨 => 얇은 복사(shallow copy)
    - 새로운 공간에 기존 객체의 주소값과 상관없는 새로운 객체를 만들어야함 => 깊은 복사(deep copy)
2. 기존 객체는 수정되면 안된다.
3. 새로 만들어진 객체들은 Tree Class의 instance여야 한다.


1번을 구현하기 위해 deep copy를 구글링하여 찾아보았다.  
JSON.stringify를 사용하여 객체를 문자로 바꾸고, JSON.parse를 이용하여 문자를 객체로 다시 바꿔주면 복사한 객체와 연결이 끊긴다고한다.  
- JSON.parse(JSON.stringify(this))  

드디어 이제 문제를 푸는가싶어 기쁜마음으로 코드를 아래와 같이 작성하였다.  

```js
let cloneObj = new Tree();
Object.assign(cloneObj, JSON.parse(JSON.stringify(this)));
```

그런데..루트 노드의 constructor만 Tree로 설정되있고, 자식노드들은 Object로 되어있다..  
![image.png](https://images.velog.io/post-images/yhe228/35220f10-223f-11ea-8a8a-754eee579194/image.png)  

assign을 통해 Tree의 Instance에 JSON.parse(JSON.stringify(this))를 연결해주면 Prototype이 모든 노드에 상속되는줄 알았는데.. 루트 노트에만 상속된다..  

모든 노드를 순회하면서 Tree의 Instance로 바꿔주려면 어떻게 해야하는지..도무지 감이 안잡힌다.  

그래서 결국 몇시간을 고민하며 시도해보다가.. 결국 답지를 보았다.. ㅜ  

reference 코드 전문이다.  

```js
var Tree = function(value) {
  this.value = value;
  this.children = [];
};

Tree.prototype.addChild = function(child) {
  if (!child || !(child instanceof Tree)) {
    child = new Tree(child);
  }
  this.children.push(child);
  // return the tree for convenience
  return this;
};

Tree.prototype.map = function(callback) {
  return this.children.reduce(function(tree, child) {
    return tree.addChild(child.map(callback));
  }, new Tree(callback(this.value)));
};
```

자 이제 내가 고민하고 고민했던 map 메소드를 분석해보자.  

```js
Tree.prototype.map = function(callback) {
  return this.children.reduce(function(tree, child) {
    return tree.addChild(child.map(callback));
  }, new Tree(callback(this.value)));
};
```

### 😊 reference 분석 
1. 루트 노드의 자식노드가 담긴 배열의 각 자식노드에 리듀스를 실행한다.
2. 이때 초기값(initial value) 은 루트 노드의 value를 인자로 받은 callback 함수를 실행한 결과값으로 만들어진 새로운 트리노드이다.
3. 각각의 자식노드에 리듀스를 실행하면 
    1. 첫번째로 현재 자식노드의 자식노드배열의 각 자식 요소에 리듀스 메소드를 실행한다.
    2. 이때 초기값(initial value)은 현재 자식 노드의 value를 인자로 받은 callback 함수를 실행한 결과값으로 만들어진 새로운 트리노드이다.
    3. 만약 현재 자식노드의 자식노드배열이 빈배열이라면 reduce를 실행해 줄 요소들이 없기때문에 초기값만 반환하여 map 메소드를 종료하고 빠져나온다.
4. 현재 초기값(initial value)에 3번에서 얻은 반환값인 새로운 트리노드를 인자로 넣고 addChild 메서드를 적용시킨다.
5. addChild 메서드를 실행한 현재 초기값(initial value)이 this가 되고 이 this의 children에 3번에서 얻은 반환값인 새로운 트리노드를 push한다.
6. 그리고 this를 반환 한다.
7. addChild 메서드 실행이 끝나고 reduce로 돌아오면 반환된 this가 다음 자식 요소에 reduce를 실행할때 누적값(accumulate)이 된다.



```js
var identity = function(value) {
  return value;
};
var input = new Tree(1);
input.addChild(2);
input.addChild(3);

var result = input.map(identity);
```
### map method 실행순서
- 현재 input = {value : 1, children : [{value : 2, children : []}, {value : 3, children : []}]}  
0. map 메소드 실행
1. 첫번째 누적값 = Tree {value : 1, children : []}
2. 두번째 누적값 = Tree {value : 1, children : [{value : 2, children : []}]}
3. 세번째 누적값 = Tree {value : 1, children : [{value : 2, children : []}, {value : 3, children : []}]}

### 😒 나의 문제점
- 나는 계속 이미 만들어져 있는 객체자체를 전부 복사해서 그 상태에서 프로토타입을 Tree로 바꿔줄 생각만 계속 했다..  
- 한가지 방법만 생각한다
- callback 함수를 재귀함수 안에서 실행시켜 return 해주려고 하니 계속 for문이 loop를 돌지않고 callback함수를 한번 돌고 return으로 끊겨 버리니 대체 어떻게하면 재귀함수처럼 loop를 도는 코드 안에서 callback을 return할까.. 이 생각만 계속했다. callback 함수를 실행시켜 반환된 값을 이용해 새로운 인스턴스 객체를 만들면 되는 것을..! callback 함수가 해당 코드에서 어떠한 역할을 하는지 제대로 파악을 못하고 코드를 작성하여 잘못된 방향으로 접근한 것 같다. 다음부터는 테스트코드를 통해 메소드나 callback 함수의 사용 의도를 확실하게 파악한 후 코드작성에 들어가야겠다. 
