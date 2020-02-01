---
title: "Event Loop?"
categories:
  - JavaScript
---

## 자바스크립트 엔진
- 자바스크립트 엔진의 대표적인 예는 Google V8 엔진이다.
- V8 은 Chrome과 Node.js에서 사용한다.
- 엔진의 주요 두 구성요소
    - Memory Heap : 메모리 할당이 일어나는 곳
    - Call Stack : 코드 실행에 따라 호출 스택이 쌓이는 곳
	![Screenshot from 2020-02-01 14-17-57.png](https://images.velog.io/post-images/yhe228/468a5600-44b2-11ea-b0c8-f5027889152a/Screenshot-from-2020-02-01-14-17-57.png)
    [이미지 출처 : 캡틴판교 블로그]
    
## 자바스크립트 런타임
![Screenshot from 2020-02-01 14-21-12.png](https://images.velog.io/post-images/yhe228/c2219670-44b2-11ea-856e-a145bb1d5c1d/Screenshot-from-2020-02-01-14-21-12.png)  
    
### Web API
  - javascript가 실행되는 런타임 환경에 존재하는 별도의 API이다
  - DOM, Ajax, setTimeout 과같이 브라우저에서 제공하는 API 들을 Web API라고 한다.
  - 브라우저에서 제공하는 API는 자바스크립트에서 호출할 수 있는 스레드를 효과적으로 지원한다.
  - Web API는 작동이 완료되면 콜백을 테스크 큐에 밀어 넣는다.

    
## 호출스택(Call Stack)이 하는 일
- 자바스크립트는 기본적으로 싱글 쓰레드 기반 언어이다. 
	- 싱글 쓰레드  : 호출 스택이 하나이기 때문에 한 번에 한 작업만 처리할 수 있다.
- Stack의 역할    
  1. 함수를 실행하면 스택에 해당 함수를 집어넣는다
  2. 함수의 실행이 끝날 때(리턴 값을 돌려줄 때) 스택의 가장 위쪽에서 해당 함수를 꺼낸다 => 해당 함수는 호출 스택에서 제거된다.

## 동시성(Concurrency) & 이벤트 루프(Event Loop)
호출 스택에 처리 시간이 오래걸리는 함수가 있을 경우,
호출 스택에서 해당 함수가 실행되는 동안 브라우저는 아무 작업도 못하고 대기 상태가 된다. 이렇게되면
브라우저는 페이지를 그리지도 못하고, 어느 코드도 실행을 못하는 상태가 된다.

- 콜스택에 어떠한 것들이 남아있으면 동기적으로 실행되는 네크워크 요청이 콜스택을 `blocking`하여 브라우저는 다른 일들을 할 수 없다. 렌더링이나 다른 코드를 실행하지 못하고 그냥 멈춰버린다.
	- blocking : 느린코드가 스택에 남아있는것
- `비동기 콜백`을 사용하면 페이지 렌더링 동작을 방해하지 않고 브라우저의 응답도 끊지 않으면서 연산량이 많은 코드를 실행할 수 있다.
        
> 스택에 필요없는 느린 코드를 쌓아서 브라우저가 할일을 못하게 만들지 말아라, 유동적인 UI를 만들어라

## 이벤트루프의 역할?
- 콜스택과 테스크 큐를 주시하는 것
- 스택이 비어있으면 큐의 첫번째 콜백을 스택에 쌓아 효과적으로 실행할 수 있게 해준다.    
- 아래의 코드처럼 0초뒤에 함수를 실행하는 코드를 작성하는 이유는?
	- 스택이 비어있을때까지 기다리게 하기 위해서
```js
setTimeout(function() {
  console.log('hi')
}, 0);
```    
    
## 콜백
- 다른함수가 부르는 함수	
- 앞으로 큐에 쌓일 비동기식 콜백

## 참고자료
- [참고영상 - 어쨌든 이벤트 루프는 무엇입니까? | Philip Roberts | JSConf EU](https://youtu.be/8aGhZQkoFbQ)
- [참고블로그 - (Captain Pangyo) 자바스크립트의 동작원리: 엔진, 런타임, 호출 스택](https://joshua1988.github.io/web-development/translation/javascript/how-js-works-inside-engine/) 
- [참고블로그 - 2](https://velog.io/@wan088/JavaScript-EventLoop%EC%99%80-%EB%B9%84%EB%8F%99%EA%B8%B0-%EB%8F%99%EC%9E%91)
