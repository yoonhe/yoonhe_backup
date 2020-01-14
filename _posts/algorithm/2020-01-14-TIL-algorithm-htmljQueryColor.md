---
title: "Toy Problem 10번 - htmljQueryColor"
categories:
  - algorithm
---

p태그 안에 모든 단어들을 span으로 감싸주고 각 단어를 초당 1회씩 color를 변경시켜주는 문제이다

## 01. 풀이

```js
$(function() {
  // --------------STEP 1--------------
  // wrap every word in every `<p>` tag with a `<span>` tag.
  // for example: <p>Hey there</p>
  // becomes: <p><span>Hey</span><span>there</span></p>
  // HINT: the `split` array method is your friend
  // TODO: your code here!
  // --------------STEP 2--------------
  // Next, change spans to random colors, once per second
  // TODO: your code here!

  /**
   * 0. p 노드들을 가져온다
   * 1. p 노드들을 순회한다
   * 2. 각각의 P 노드의 text content를 split(' ')을 통해 단어배열로 만든다
   * 5. 단어배열을 순회한다.
   * 6. 각 단어요소를 텍스트로 가지는 span 노드를 만들어준다
   * 7. P 노드에 append 해준다 
   * 8. span 노드들을 불러온다
   * 9. span 노드들을 순회한다
   * 10. 각 span 노드가 똑같이 컬러가 바뀌지 않도록 노드의 index의 * 50에 해당하는 시간 뒤에 실행되도록 해준다
   */
  let nodeP = $("p");

  Array.prototype.forEach.call(nodeP, function(nodePElem) {
    let strs = nodePElem.textContent.split(" ");

    nodePElem.textContent = "";
    strs.forEach(elem => {
      let spanNode = makeSpan(elem);
      nodeP.append(spanNode);
    });
  });

  let spans = $("span");
  for (let i = 0; i < spans.length; i++) {
    setTimeout(function() {
      spans.eq(i).css("color", "black");
    }, i * 50);
  }

  function makeSpan(text) {
    let $span = $("<span>" + `${text} ` + "</span>");
    $span.css("color", "gray");
    return $span;
  }
});
```
## 02. animate에서 color 속성 사용 에러문제 😱

Jquery로 작성해야 테스트가 통과한다고 하여 color 바꿔주는 부분을 jQuery animate와 delay를 사용해서 작성도 해보았다.

```js
spans.each(function(index) {
  spans
    .eq(index)
    .delay(index * 10)
    .animate({
    // fontSize: "20px",
    color: "black"
  });
});
// => fontSize는 animate가 적용되는데 font-size는 왜 적용이 안될까?..
```
그런데 animate 사용하면 fontSize 속성은 변경되는데 color는 변경이 안되는 것이다.. 이유를 모르겠어서 구글에 'jquery animate color not working'이라고 검색 해보았다.  
구글링을 해보니 
> jQuery Core는 기본 색상 애니메이션을 지원하지 않습니다. animate () 호출이 예상대로 작동하려면 jQuery UI 또는 독립 실행 형 jQuery 색상 플러그인과 같은 것을 사용해야합니다.

라고 [stackoverflow](https://stackoverflow.com/questions/13461984/jquery-animate-not-working-with-colors)에 답글이 달려있었다.  

아래와 같이 [jQuery-ui](https://jqueryui.com/animate/)를 따로 불러와주니 color도 animate가 지원이 되었다.

```html
<head>
  <script src="lib/jquery.js"></script>
  <script src="https://code.jquery.com/ui/1.12.1/jquery-ui.js"></script> <!-- 추가 -->
  <script src="main.js"></script>
</head>
```

예전에 퍼블리셔로 일할때 vanilla javascript는 모르는 상태로 jQuery를 사용했었는데 이제 vanilla javascript를 배우면서 jQuery를 사용할 일이 없다보니 이제는 jQuery가 너무 생소해져서 기억을 되살리려 몇가지 기능을 찾아보았다.

## 03. jQuery로 노드 다루는 방법
1. 노드 생성

	```js
    // $("추가노드DOM 문자열")
    let $span = $("<span>" + `${text} ` + "</span>");
	let $li=$("<li>new menu</li>");
	```
    
2. 노드에 스타일 지정

	```js
	let $span = $("<span>" + `${text} ` + "</span>");
    $span.css("color", "gray"); // set
    $span.css("color"); // gray => get
	```
    
3. append
	신규 노드를 특정 노드의 마지막 번째 자식 노드로 추가하기
    
	```js
	// $부모노드.append($신규노드)
	// $신규노드.appendTo($부모노드)

	let nodeP = $("p");
	let spanNode = makeSpan(elem);
    nodeP.append(spanNode);
 
	function makeSpan(text) {
      let $span = $("<span>" + `${text} ` + "</span>");
      $span.css("color", "gray");
      return $span;
    }
	```
    
4. prepend
	신규 노드를 첫 번째 자식 노드로 추가

    ```js
	// $부모노드.prepend($추가노드)
    // $추가노드.prependTo($부모노드)

	var $li=$("<li>menu</li>");            
    $("ul.menu").prepend($li);
    ```

5. before
	특정 노드의 이전 위치에 추가   
	![image.png](https://images.velog.io/post-images/yhe228/58cb4c40-36aa-11ea-8479-9936b949728a/image.png)
    
    ```js
	// $추가노드.insertBefore($기준노드)
    // $기준노드.before($추가노드)
	let test = $('.test')
	test.before('<p>yoonhe</p>');
	```

5. after
	특정 노드 다음에 노드 추가  
	![image.png](https://images.velog.io/post-images/yhe228/2163fd50-36ab-11ea-b628-a7fbcba27138/image.png)

    ```js
	// $추가노드.insertAfter($기준노드)
	// $기준노드.after($추가노드)

	let test = $('.test')
	test.after('<span>after</span>');
	```
    
    
 ### 🧚‍♀️ [참고블로그](https://m.blog.naver.com/PostView.nhn?blogId=kimnx9006&logNo=220587687239&proxyReferer=https%3A%2F%2Fwww.google.com%2F)
