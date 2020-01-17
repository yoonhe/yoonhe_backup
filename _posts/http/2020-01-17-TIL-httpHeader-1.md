---
title: "HTTP 공통 & 요청 헤더"
categories:
  - HTTP
---

## 공통헤더
요청과 응답에 모두 사용되는 헤더이다.

### Date
HTTP 메시지가 만들어진 시각. 자동으로 만들어진다.  
![image.png](https://images.velog.io/post-images/yhe228/0ce5b140-392e-11ea-857f-85d9b3abf241/image.png)

### Content-Length
요청과 응답 메시지의 본문 크기를 바이트 단위로 표시해준다. 메시지 크기에 따라 자동으로 만들어진다.  
![image.png](https://images.velog.io/post-images/yhe228/87085310-392e-11ea-ac73-97a79f467172/image.png)

### Content-Type
- Content-Type: text/html; charset=utf-8
	- 현재 메시지 내용이 text/html 타입이고 문자열은 utf-8 문자열임을 알려준다.
- 컨텐츠의 타입(MIME)과 문자열 인코딩(utf-8 등등)을 명시할 수 있다.
- Accept 헤더, Accept-Charset 헤더와 대응된다.
- 프론트엔드에서 서버로 데이터를 보낼 때는 text/html 이런 것 대신 www-url-form-encoded나 multipart/form-data같은 게 Content-Type이 된다.  
![image.png](https://images.velog.io/post-images/yhe228/ffd10a30-392e-11ea-ac73-97a79f467172/image.png)  

### Content-Language
- 사용자의 언어를 뜻한다.
- 요청이나 응답이 무슨 언어인지와는 관련 없다.
- 예를 들어 한국 사람한테 일본어를 가르치는 사이트일 경우, 페이지 언어는 일본어더라도 Content-Language는 ko-KR일 수 있다.  
![image.png](https://images.velog.io/post-images/yhe228/2a3a2040-392f-11ea-9946-1dce64e3fe83/image.png)

### Content-Encoding
- Content-Encoding: gzip, deflate
- Content-Encoding은 컨텐츠 압축된 방식이다.
- 응답 컨텐츠를 br, gzip, deflate 등의 알고리즘으로 압축해서 보내면, 브라우저가 알아서 해제해서 사용한다.
- 이 외에도 다양한 압축 알고리즘이 존재한다. 컨텐츠 용량이 줄어들기 때문에 압축을 권장한다.
- 압축을 하면 요청이나 응답 전송 속도도 빨라지고, 데이터 소모량도 줄어들기 때문에 가능하면 압축을 해두는 것이 좋다.


## 요청 헤더
### Host
- 서버의 도메인 네임이 나타나는 부분입니다(포트 포함). 
- Host: www.zerocho.com
- Host 헤더는 반드시 하나가 존재해야 합니다.
![image.png](https://images.velog.io/post-images/yhe228/5edf5710-3930-11ea-a83d-8f80807e9615/image.png)

### User-Agent
- Host보다 더 유명한 헤더는 User-Agent이다.
- 현재 사용자가 어떤 클라이언트(운영체제와 브라우저 같은 것)를 이용해 요청을 보냈는지 나온다.
- User-Agent 헤더를 활용해서 접속자 통계를 낼 수 있다.
- User-Agent 헤더를 활용해서 IE로 접속한 사람들을 찾아낸 후, IE는 지원하지 않으니 크롬으로 접속해주세요와 같은 메시지를 표시하기도 한다.
![image.png](https://images.velog.io/post-images/yhe228/adf6fd80-3930-11ea-ac73-97a79f467172/image.png)

### Accept
- Accept 헤더는 요청을 보낼 때 서버에 이런 타입(MIME)의 데이터를 보내줬으면 좋겠다고 명시할 때 사용한다.
- 예를 들어 요청의 헤더로 `Accept: text/html`를 보내면 HTML 형식인 응답을 처리하겠다는 뜻이다.
- 콤마로 여러 타입을 동시에 적어줄 수도 있고, *(와일드카드)로 "텍스트이기만 하면 돼"라고 적어줄 수도 있다.

    ```
    Accept: image/png, image/gif
    Accept: text/*
    ```

![image.png](https://images.velog.io/post-images/yhe228/c2314ba0-3932-11ea-afd5-1bd0fa67b500/image.png)


#### Accept 시리즈
공통 헤더의 Content 시리즈와 대응된다. Accept로 원하는 형식을 보내면, 서버가 그에 맞춰 보내주면서 응답 헤더의 Content를 알맞게 설정한다.

![image.png](https://images.velog.io/post-images/yhe228/7fb640a0-3932-11ea-af23-957dffceb707/image.png)

1. Accept-Encoding : 원하는 컨텐츠 압축 방식
	- ex) Accept-Encoding: br, gzip, deflate
2. Accept-Charset : 문자 인코딩(UTF-8 등)을 명시한다.
	- ex) Accept-Charset: utf-8
3. Accept-Language : 원하는 언어
	- ex) Accept-Language: ko, en-US

뭘 적어야할지 모르겠다면,  
1. *(와일드카드)를 적거나, 
2. 그냥 브라우저가 알아서 설정해서 보내는 Accept를 사용하면 된다.

### Authorization
- Authorization 헤더는 인증 토큰(JWT든, Bearer 토큰이든)을 서버로 보낼 때 사용하는 헤더이다.
- API 요청같은 것을 할 때 토큰이 없으면 거절당하기 때문에 이 때, Authorization을 사용하면 된다.
	- ex) Authorization: Bearer XXXXXXXXXXXXX
	- 보통 Basic이나 Bearer같은 토큰의 종류를 먼저 알리고 그 다음에 실제 토큰 문자를 적어 보낸다.
    
### Origin
- POST같은 요청을 보낼 때, 요청이 어느 주소에서 시작되었는지를 나타낸다.
- 여기서 요청을 보낸 주소와 받는 주소가 다르면 CORS 문제가 발생한다.

### Referer
- Referer: https://www.zerocho.com/category/JavaScript
- 이 페이지 이전의 페이지 주소가 담겨 있다.
- 이 헤더를 사용하면 어떤 페이지에서 지금 페이지로 들어왔는지 알 수 있기 때문에 애널리틱스같은 데 많이 사용된다.  
![image.png](https://images.velog.io/post-images/yhe228/43984770-3933-11ea-afd5-1bd0fa67b500/image.png)

