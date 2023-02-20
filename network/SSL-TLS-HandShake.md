## ✔️ 들어가기 전...

> **HTTPS****는** 애플리케이션 계층과 전송 계층 사이에   
> 신뢰 계층인 **TLS / SSL 계층을 넣은 신뢰할 수 있는 HTTP 요청**을 말한다.  
>   
> → 이를 통해 '통신을 암호화' 한다.

※ 참고 : 향상된 TCP 버전을 SSL이라 부르고, SSL의 약간 변형된 버전이 TLS(표준화됨)이다.

더보기

SSL(Secure Socket Layer)은 SSL 1.0부터 시작해서 

SSL 2.0, SSL 3.0, TLS(Transport Layer Security Protocol) 1.0, TLS 1.3까지 

버전이 올라가며 마지막으로 TLS로 명칭이 변경되었으나, 

**보통 이를 합쳐 SSL/TLS로 많이 부른다**.

## ✔️ 대칭키 암호화 vs 공개키 암호화(비대칭 암호화)

💡 대칭키 암호화

![](https://blog.kakaocdn.net/dn/LNk00/btrZqTaUFmK/Qet29rOniGyQNM1t2AMBCK/img.gif)

> 대칭키 암호란, 암호화에 사용되는 키와 복호화에 사용되는 키가 동일한 기법이다.  
>   
> 그렇기 때문에 암호화한 정보를 보낼 때 암호키를 같이 보내야 해서   
> 타인에게 노출되는 경우 보안에 취약하다는 단점이 있다.  
>   
> 키 전달 관리에 어려움이 있지만, 대칭키 암호화는 연산 속도가 빠르다는 장점이 있다.

🚨 대칭키가 가지는 해킹의 위협을 막고자 나온 것이 **공개키(Public Key)**이다.

**암호화와 복호화에 사용하는 키를 분리하는 방식**이다.

💡 공개키 암호화(비대칭키 암호화)

![](https://blog.kakaocdn.net/dn/dHR4B0/btrZtrqGPIY/IRnLSlzznNwEGPKMazmEc1/img.gif)

> \- 대칭 암호화 방식 : 비밀키 하나만 가짐.  
> \- 공개키(비대칭) 암호화 : 공개키 + 비밀키, 두 개 존재.  
>   
> 즉, **누구에게나 공개 가능한 공개키 + 자신만이 갖고 있는 개인키.**

> 1\. **공개키**로 암호화하는 경우  
> \- 상대방의 공개키로 데이터를 암호화하고 전달하면,   
> 데이터를 전달받은 사람은 자신의 개인키로 데이터를 복호화한다.  
>   
> 2\. **개인키**로 암호화하는 경우  
> \- 개인키의 소유자가 개인키의 데이터를 암호화하고 공개키와 함께 전달한다.  
> 이 과정에서 공개키와 데이터를 획득한 사람은 공개키를 이용해서 복호화를 한다.  
> → 데이터의 보호 목적보다는, 공개키가 데이터 제공자의 신원 보장하기 위함이다.  
>   
> 암호회된 데이터가 공개키로 복호화된다는 것은,   
> 공개키와 쌍을 이루는 개인키에 의하여 암호화되었다는 것을 뜻한다.  
> 즉, 데이터 제공자의 신원 확인이 보장된다는 뜻이기 때문에 전자서명에 이용한다.

---

## ✔️ SSL / TLS

> SSL/TLS는 전송 계층에서 보안을 제공하는 프로토콜이다.  
>   
> 클라이언트와 서버가 통신할 때, SSL/TLS를 통해 제 3자가 메시지를 도청하거나 변조하지 못하도록 한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcGb0IQ%2FbtrZxJK1twt%2FlcBNLemplGxyxNP4uUnsAK%2Fimg.png)

> 위의 그림처럼 SSL/TLS를 통해 공격자가 서버인 척하며   
> 사용자 정보를 가로채는 네트워크상의 '인터셉터'를 방지할 수 있다.  
>   
> SSL/TLS는 보안 세션을 기반으로 **데이터를 암호**화한다.  
> 따라서 데이터를 가로채려해도 거의 **복호화가 불가능**하다.  
> ※ 보안 세션 : 보안이 시작되고 끝나는 동안 유지되는 세션을 말하고, SSL/TLS는 **핸드셰이크를 통해 보안 세션을 생성**하고 이를 기반으로 상태 정보 등을 공유한다.

---

## ✔️ SSL/TLS HandShake

> 핸드셰이크는 클라이언트와 서버간의 메세지 교환이며, HTTPS 웹에 처음 커넥션할 때 진행된다.

💡 SSL/TLS 핸드셰이크 요약

1.  브라우저가 SSL/TLS 보안 웹 사이트를 열고 웹 서버에 연결한다.
2.  브라우저는 식별 가능한 정보를 요청하여 웹 서버의 진위 여부를 확인하려고 시도한다.
3.  웹 서버는 공개 키가 포함된 SSL/TLS 인증서를 회신으로 보낸다.
4.  브라우저는 SSL/TLS 인증서가 유효하고, 웹 사이트 도메인과 일치하는지 확인한다.
5.  브라우저가 SSL/TLS 인증서에 만족하면 공개키를 사용하여 비밀 세션 키가 포함된 메시지를 암호화하고 전송한다.
6.  웹 서버는 개인키를 사용하여 메시지를 해독하고 세션키를 검색한다.
7.  그런 다음 세션키를 사용하여 암호화하고, 브라우저에 승인 메시지를 보낸다.
8.  이제 브라우저와 웹 서버 모두 동일한 세션 키를 사용하여 메시지를 안전하게 교환하도록 전환한다.

※ SSL/TLS 인증서 : CA(Certificate Authority)

더보기

SSL은 SSL 인증서(=TLS 인증서)가 있는 웹사이트만 실행할 수 있다.

인증서는 신분증과 유사하다고 볼 수 있다.

SSL 인증서에는 공개키가 포함된다. **이 공개키 덕분에 암호화가 가능**하다.

클라이언트의 요청은 공개키를 이용해 서버에 암호화 하여 전달한다.

서버에도 공개되지 않는 개인 키가 있는데, 이 개인키를 이용해 암호화된 데이터를 복호화한다.

해당 인증서를 발급하는 기관은 **CA(Certificate Authority)**라고 한다.

좀 더 자세히 알아보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbms0Gh%2FbtrZqAinxjz%2FgF2szdIdOnZ2PbI0z7bUok%2Fimg.png)

1.  클라이언트는 서버에게 "client hello" 메시지를 담아 서버로 보낸다.
    -   이때 암호화된 정보를 함께 담는데, '버전', '암호 알고리즘', '압축 방식' 등을 담는다.
2.  서버는 클라이언트가 보낸 암호 알고리즘과 압축 방식을 받고, 세션 ID와 CA 공개 인증서를 "server hello" 메시지와 함께 담아 응담한다.
    -   이 CA 인증서에는 앞으로 통신 이후 사용할 대칭키가 생성되기 전, 클라이언트에서 handshake 과정 속 암호화에 사용할 공개키를 담고있다.
3.  클라이언트는 서버에서 보낸 CA 인증서에 대해 유요한지 CA 목록에서 확인하는 과정을 진행한다.
4.  CA 인증서에 대한 신뢰성이 확보되었다면, 클라이언트는 난수 바이트를 생성하여 서버의 공개키를 암호화한다.
    -   이 난수 바이트는 대칭키를 정하는데 사용이 되고, 앞으로 서로 메시지를 통신할 때 암호화하는데 사용된다.
5.  만약 2번 단계에서 서버가 클라이언트 인증서를 함께 요구했다면, 클라이언트의 인증서와 클라이언트의 개인키로 암호화된 임의의 바이트 문자열을 함께 보내준다.
6.  서버는 클라이언트의 인증서를 확인 후, 난수 바이트를 자신의 개인키로 복호화 후 대칭 마스터 키 생성에 활용한다.
7.  클라이언트는 handshake 과정이 완료되었다는 "finished" 메시지를 서버에 보내면서, 지금까지 보낸 교환 내역들을 해싱 후 그 값을 대칭키로 암호화하여 같이 담아 보내준다.
8.  서버도 동일하게 교환 내용들을 해싱한 뒤 클라이언트에서 보내준 값과 일치하는 지 확인한다.
    -   일치하면 서버도 마찬가지로 "finished" 메시지를 이번에 만든 대칭키로 암호화하여 보낸다.
9.  클라이언트는 해당 메시지를 대칭키로 복호화하여 서로 통신이 가능한 신뢰받은 사용자란 걸 인지하고, 앞으로 클라이언트와 서버는 해당 대칭키로 데이터를 주고받을 수 있게 된다.

---

### 출처

-   컴퓨터 네트워킹 하향식 접근 제 7판
-   [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Network/TLS%20HandShake.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Network/TLS%20HandShake.md)
-   [https://www.digicert.com/kr/what-is-ssl-tls-and-https](https://www.digicert.com/kr/what-is-ssl-tls-and-https)
-   [https://kanoos-stu.tistory.com/46](https://kanoos-stu.tistory.com/46)
-   [https://aws.amazon.com/ko/what-is/ssl-certificate/](https://aws.amazon.com/ko/what-is/ssl-certificate/)
-   [https://m.blog.naver.com/sung\_mk1919/221598350824](https://m.blog.naver.com/sung_mk1919/221598350824)
-   [https://wangin9.tistory.com/entry/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EC%97%90-URL-%EC%9E%85%EB%A0%A5-%ED%9B%84-%EC%9D%BC%EC%96%B4%EB%82%98%EB%8A%94-%EC%9D%BC%EB%93%A4-5TLSSSL-Handshake](https://wangin9.tistory.com/entry/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EC%97%90-URL-%EC%9E%85%EB%A0%A5-%ED%9B%84-%EC%9D%BC%EC%96%B4%EB%82%98%EB%8A%94-%EC%9D%BC%EB%93%A4-5TLSSSL-Handshake)