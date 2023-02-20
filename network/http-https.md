# **HTTP**

> HyperText Tranfer Protocol로 WWW상에서 정보를 주고 받는 프로토콜이다. 서버-브라우저 데이터를 전송하는 용도로 가장 많이 사용한다.  
> Method, Path, Version, Headers, Body 등으로 구성된다.

-   Tim Berners Lee가 1991년에 발명하였다.
-   HTTP는 **웹 브라우저(Client)와 서버(Server)** 간의 데이터를 주고 받을 때 사용하는 **애플리케이션 레이어 프로토콜(통신 규약)**을 말한다.
-   HTTP는 클라이언트가 요청을 하기 위해 연결을 연 다음 응답을 받을때 까지 대기하는 전통적인 클라이언트-서버 모델을 따른다.
-   HTTP통신은 클라이언트가 데이터를 요청(request)하면 그 요청을 처리하여 서버가 다시 클라이언트에게 응답(response)하는 큰 흐름을 가진다.
-   HTTP는 `무상태stateless 프로토콜`로 서버가 두 요청 간에 어떠한 데이터도 유지하지 않는다. 👉 별도로 쿠키와 세션을 사용하는 이유가 된다.
-   기본적으로 80번 포트를 사용하고 있다.

> **✅ 클라이언트-서버 프로토콜**  
> \- 클라이언트 : 통신 시작자  
> \- 서버 : 클라이언트로부터 통신 요청을 받는 수신자  
> (보통 웹브라우저인) 수신자 측에 의해 요청이 초기화되는 프로토콜을 의미한다.

> **✅ 무상태 프로토콜 stateless protocol [참고링크](https://ko.wikipedia.org/wiki/%EB%AC%B4%EC%83%81%ED%83%9C_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)**  
> 이전 요청과 무관한 각각의 요청을 독립적인 트랜잭션으로 취급하는 통신 프로토콜. 통신이 독립적인 쌍의 '요청-응답' 을 이룰 수있게 하는 방식이다. 각각의 통신 파트너에 대한 세션 정보나 상태 보관을 요구하지 않는다.
> 
> ↔️ 상태 프로토콜 stateful protocol

## **HTTP 요청 Request 구조**

> 크게 Request Line, Request Headers, Request Message Body로 구분된다.

![](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview/http_request.png)

-   `Request Line` : 메서드, 요청 리소스, 프로토콜 버전이 포함된다.
-   `Request Headers` : 서버에서 추가 정보를 전달한다. `key:value` 값으로 되어 있다.
-   `Request Message Body` : request에 대한 실제 메시지/데이터가 있다. 필요 없으면 생략한다.

#### **method**

```
- 데이터를 어떻게 보낼지를 정의한다. 필수로 지정해주어야 한다.
```

**`GET` **⭐️****

-   서버로부터 데이터를 가져올 때 사용한다. 오직 데이터를 받기만 한다.
-   HTML, css, json, xml 등 대부분 데이터를 가져올 수 있다.
-   `GET`을 사용하면 응답시 정보가 URL에 노출되므로, 민감한 정보 통신은 `POST` 방식을 사용한다.

**`POST` **⭐️****

-   클라이언트가 서버에 데이터를 새로 추가할 때 사용한다.
-   로그인, 블로그 글쓰기 등은 `POST`를 사용해서 작성한다.
-   민감한 정보 (비밀번호, 신용카드번호 등)을 전송할 때도 사용한다.
-   POST로 전송된 정보는 one-time action으로 북마크되지 않는다. (URL에 드러나지 않는다.)

**`HEAD`** GET 메서드와 동일한 응답을 요청하지만, 응답 본문을 포함하지는 않는다.

**`PUT`** 서버에 이미 존재하는 데이터를 업데이트 할 때 사용한다.

**`DELETE`** 서버의 특정 리소스를 삭제할 때 사용한다.

**`CONNECT`** 목적 리소스로 식별되는 서버로 터널을 맺는다.

**`OPTIONS`** 해당 엔드포인트가 어떤 http 메소드를 서포트하는지 모를 때, 메소드의 정보를 요청하기 위해 사용한다.

**`PATCH`** 리소스의 일부 부분을 수정하는 데 쓰인다.

### **headers**

-   `Host` : 요청 target의 host url
-   `User-Agent` : 요청을 보내는 클라이언트의 대한 정보: 사용하는 웹 브라우저와 버전, OS 등
-   `Accept` : 해당 요청이 받을 수 있는 응답(response) 타입. (조건부 요청을 허용: (accept-, If-), 모든 요청 허용:(/))
-   `Connection` : 해당 요청이 끝난후에 클라이언트와 서버가 계속해서 네트워크 컨넥션을 유지 할것인지 아니면 끊을것인지에 대해 지시하는 부분. (Keep-alive or cancel)
-   `Content-Type` : 해당 요청이 보내는 메세지 body의 타입. 예를 들어, JSON을 보내면 application/json.
-   `Content-Length` :메세지 body의 길이.


## **HTTP Response 구조**

> 주로 다음과 같이 구성됩니다. protocol version, Status Code, headers, body

![](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview/http_response.png)

-   HTTP 프로토콜의 버전
-   요청의 성공 여부와, 그 이유를 나타내는 상태 코드
-   아무런 영향력이 없는, 상태 코드의 짧은 설명을 나타내는 상태 메시지
-   요청 헤더와 비슷한, HTTP 헤더들
-   선택 사항으로 가져온 리소스가 포함되는 본문

---

# **HTTPS**

> Hypertext Transfer Protocol Secure  
> HTTP + Secure  
> 서버와 브라우저 사이에 암호화된 연결을 만들 수 있게 도와주고, 정보가 도난당하는 것을 막아준다.

-   HTTP가 중간에 정보를 도난당할 수 있는 단점을 보완한 방식으로 현재 많은 웹사이트에서 사용하고 있다.
-   클라이언트와 서버 간의 모든 커뮤니케이션을 암호화 하기 위하여 `SSL` 이나 `TLS`을 사용한다.
-   금융이나 온라인 쇼핑 등 클라이언트와 서버가 민감한 정보를 주고받을 수 있도록 해준다.

![](https://velog.velcdn.com/images%2Faverycode%2Fpost%2Fc056bac3-596c-4890-82d4-c8b5537d6f0d%2Fimage.png)

## **SSL**

> Secure Sockets Layer 보안 소켓 계층

-   Netscape Communications Corporation 에서 웹서버와 웹 브라우저간의 보안을 위해 만든 프로토콜
-   기능
    -   서버와 브라우저 사이에 안전한 암호화된 연결을 만들 수 있게 도와준다.
    -   민감한 정보를 주고받을 때 해당 정보가 도난당하는 것을 막아준다.
    -   HTTP 메시지 body를 암호화 하는 방식으로, header는 암호화되지 않는다.
-   비대칭키와 대칭키를 혼합하여 사용한다. [참고링크](https://velog.io/@gs0351/%EB%8C%80%EC%B9%AD%ED%82%A4-vs-%EA%B3%B5%EA%B0%9C%ED%82%A4%EB%B9%84%EB%8C%80%EC%B9%AD%ED%82%A4)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FGTThC%2FbtrZ7q5xSme%2FvtJn0BqrIbtd5xWIghEX9K%2Fimg.png)

-   대칭키 암호화
    -   클라이언트와 서버가 동일한 키를 사용해 암호화/복호화 진행
    -   키가 노출되면 매우 위험하지만 연산 속도가 빠름


![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbPYXYS%2FbtrZSSvM4X2%2FdYELEOc9ZMjaoniu7rnTc0%2Fimg.png)

-   비대칭키 암호화
    -   1개의 쌍으로 구성된 공개키와 개인키를 암호화/복호화 하는데 사용
    -   키가 노출되어도 비교적 안전하지만 연산 속도 느림

### **SSL 통신 과정**

![](https://velog.velcdn.com/images%2Faverycode%2Fpost%2F1e192b79-3071-4de2-ad1d-1d203c399e08%2Fimage.png)

 Hand-Shaking 과정에서는 먼저 서버와 클라이언트간 세션키를 교환한다. 여기서 세션키는 주고받는 데이터를 암호화하기 위해 사용되는 대칭키이다. (데이터 간 교환에는 빠른 연산 속도가 필요하므로 세션키는 대칭키로 만들어진다.)

 처음 연결을 성립해 안전하게 세션키를 공유하는 과정에서 비대칭키가 사용된다. 이후 데이터를 교환하는 과정에서 빠른 연산 속도를 위해 대칭키가 사용된다.

1.  클라이언트가 서버로 최초 연결 시도
2.  서버는 공개키를 브라우저에게 넘김
3.  브라우저는 인증서의 유효성을 검사하고 세션키 발급
4.  브라우저는 세션키를 보관하며 추가로 서버의 공개키로 세션키를 암호화해 서버로 전송
5.  서버는 개인키로 암호화된 세션키를 복호화하여 세션키를 얻음
6.  클라이언트와 서버는 동일한 세션키를 공유하므로 데이터를 전달할 때 세션키로 암호화/복호화를 진행

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb3C0vD%2FbtrZ2z3zhbj%2FAsn64SAkTWJkjDlBesHoF0%2Fimg.png)

---

# **HTTP 와 HTTPS**

## **HTTP의 장점**

-   HTTP 페이지는 빠르게 액세스할 수 있도록 컴퓨터와 인터넷 캐시에 저장된다.

## **HTTP의 단점**

-   암호화되지 않은 평문 데이터를 전송하는 프로토콜로 비밀번호와 같은 중요한 정보를 전송하면 제 3자가 정보를 조회할 수 있어 위험하다. 👉 HTTPS가 등장하였다.

## **HTTPS 의 장점**

-   보안에 유리하다.
    -   기밀성 : 암호화와 복호화로 인증되지 않은 제3자가 정보를 읽지 못하도록 보호한다.
    -   무결성 : 중간에 변조되지 않은 정보로 전체 정보가 목적지에 도달하도록 한다.
-   검색 엔진에 유리하다.
    -   구글은 HTTPS 웹 사이트에 가산점을 준다.
    -   가속화된 모바일 페이지 AMP를 만들 때 HTTPS를 사용해야만 한다.

> **AMP?**  
> 구글에서 만든 가속화된 모바일 페이지. 모바일 친화적인 웹사이트를 만들기 위해 사용한다.

## **HTTPS의 단점**

-   인증서 발급 및 유지를 위해 추가 비용이 발생한다.
-   HTTP에 비해 느리다. 하지만 오늘날에는 거의 차이를 느끼지 못할 정도.
-   HTTPS의 경우에는 소켓(데이터를 주고 받는 경로) 자체에서 인증을 하기 때문에 인터넷 연결이 끊기면 소켓도 끊어져서 다시 HTTPS 인증이 필요하다.

## **HTTP와 HTTPS의 차이**

HTTP와 HTTPS의 가장 큰 차이는 보안성입니다. HTTP는 데이터를 암호화하지 않기 때문에, 제3자가 데이터를 가로채서 정보를 볼 수 있습니다. 반면, HTTPS는 데이터를 암호화하기 때문에, 제3자가 데이터를 가로채도 정보를 보지 못합니다. 따라서, HTTPS를 사용하면 인터넷에서 데이터를 안전하게 주고받을 수 있습니다.

또한, HTTPS를 사용하면 웹사이트에서 제공되는 콘텐츠가 더욱 안전하다는 것을 알 수 있습니다. HTTPS를 사용하는 웹사이트는 웹 브라우저 주소창에 자물쇠 모양이 나타납니다. 이는 웹사이트가 안전하게 암호화된 연결을 사용하고 있음을 나타냅니다.

---

# ref.

-   [HTTP / HTTPS](https://youtu.be/wPdH7lJ8jf0)
-   [HTTP 요청 형식 참고](https://atoz-develop.tistory.com/entry/JAVA-TCP-%EC%86%8C%EC%BC%93-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%EC%9C%BC%EB%A1%9C-%EA%B0%84%EB%8B%A8%ED%95%9C-HTTP-%ED%81%B4%EB%9D%BC%EC%9D%B4%EC%96%B8%ED%8A%B8-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0)
-   [HTTP Request 구조 참고](https://velog.io/@rosewwross/Http-and-Request-and-Response-hok6exbnfb)
-   [HTTP 주요 헤더 정보](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers)