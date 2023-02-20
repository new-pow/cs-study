## ✔️ 들어가기 전 요약

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FLTSvP%2FbtrZqAJhQzN%2Fva04qPKhcGKQt3R1Yq68q1%2Fimg.png)

\[1줄 요약\]

-   TCP와 UDP는 OSI 7 계층 중 전송 계층에서 사용되는 프로토콜이다.
    -   ※ 전송 계층은 송신자와 수신자를 연결하는 통신서비스르 제공하는 계층이다.
    -   즉, **데이터의 전달**을 담당하며, 전달되는 패킷의 오류를 검사하고 재전송 요구 등의 제어를 담당한다.
-   TCP와 UDP는 각각 **가상회선 방식**과 **데이터그램 방식**이라는 점에서 차이를 가지며, 신뢰성과 연속성 두 측면에서 상충관계에 있다.

#### 💡 TCP와 UDP의 차이

> \- **TCP**는 **연결형 서비스**로 3-way handshaking 과정을 통해 연결을 설정하기 때문에   
> **높은 신뢰성**을 보장하지만,   
> **속도가 비교적 느리다**는 단점이 있다.  
>   
> \- **UDP**는 **비연결형 서비스**로 3-way handshaking을 사용하지 않기 때문에   
> **신뢰성이 떨어지는** 단점이 있지만,   
> 데이터 수신 여부를 확인하지 않기 때문에 **속도가 빠르다**는 장점이 있다.

> \- **TCP** : **신뢰성과 순차적인 전달이 필요한 경우 사용**한다.  
> TCP 서비스는 송신자와 수신자 모두가 소켓이라고 부르는 종단점을 생성함으로써 이루어진다.  
> TCP는 멀티캐스팅이나 브로드캐스팅을 지원하지 않는다.  
>   
> \- **UDP** : 비연결형 프로토콜이며, 손상된 세그먼트의 수신에 대한 재전송을 하지 않는다.  
> UDP를 사용하는 것에는 DNS가 있다.  
> 사전에 설정이 필요하지 않으며, 그 후에 해제가 필요하지 않다.

💡 즉, TCP는 신뢰성이 중요한 파일 교환과 같은 경우에 쓰이고, 

UDP는 실시간성이 중요한 스트리밍에 자주 사용된다.

| 프로토콜 종류 | TCP | UDP |
| --- | --- | --- |
| 연결 방식 | 연결형 서비스 | 비연결형 서비스 |
| 패킷 교환 방식 | 가상 회선 방식 | 데이터그램 방식 |
| 전송 순서 | 전송 순서 보장 | 전송 순서가 바뀔 수 있음 |
| 수신 여부 확인 | 수신 여부를 확인함 | 수신 여부를 확인하지 않음 |
| 통신 방식 | 1:1 통신 | 1:1 or 1:N or N:N 통신 |
| 신뢰성 | 높다 | 낮다 |
| 속도 | 느리다 | 빠르다 |

---

네트워크의 계층들 중 전송 계층에서 사용하는 프로토콜에 대해 알아보자.

전송계층은 송신자와 수신자를 연결하는 통신서비스를 제공하는 계층으로, 

쉽게 말해 데이터의 전달을 담당한다.

그리고 **데이터를 보내기 위해 사용하는 프로토콜**이 있는데, 

그 프로토콜들이 **TCP와 UDP**이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbcjHgr%2FbtrWdfBiAJ5%2Fxxi8VHwUusbvGdr2zzmGKk%2Fimg.jpg)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbmWj7x%2FbtrWfP9FHDR%2FEtdLhLkyp6kxEDNwC6BiiK%2Fimg.png)

## ✔️ TCP (Transmission Control Protocol)

> TCP는 신뢰성 있는 데이터 전송을 지원하는 연결 지향형 프로토콜이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FOmnCy%2FbtrZtrc04G8%2Fj5hmeWc5g14hoPMFirjJS0%2Fimg.png)

> 일반적으로 TCP와 IP가 함께 사용되는데,   
> IP가 데이터의 전송을 처리한다면  
> TCP는 패킷 추적 및 관리를 하게 된다.

> 연결 지향형인 TCP는 3-way handshaking이라는 과정을 통해 연결 후 통신을 시작하는데,  
> 흐름 제어와 혼잡 제어를 지원하며 데이터의 순서를 보장한다.

## ✔️ 흐름 제어와 혼잡제어

#### 흐름 제어

> 보내는 측과 받는 측의 데이터 처리 속도 차이를 조절해주는 것

#### 혼잡 제어

> 네트워크 내의 패킷 수가 넘치게 증가하지 않도록 방지하는 것

## ✔️ TCP의 특징

1.  연결형 서비스로 가상 회선 방식을 제공
    -   3-way-handshaking 과정을 통해 연결을 설정하고, 
    -   4-way-handshaking 과정을 통해 연결을 해제한다.
2.  흐름 제어 (Flow Control)
    -   데이터 처리 속도를 조절하여 수신자의 버퍼 오버플로우를 방지
3.  혼잡 제어 (Congestion Control)
    -   네트워크 내의 패킷 수가 과도하기 증하가지 않도록 방지
4.  높은 신뢰성을 보장
    -   신뢰성이 높은 전송을 하기 때문에 UDP보다 속도가 느림
5.  전이중(Full-Duplex), 점대점(Point to Point) 방식
    -   전이중(Full-Duplex) : 전송이 양방향으로 동시에 일어날 수 있다.
    -   점대점(Point to Point) : 각 연결이 정확히 2개의 종단점을 가지고 있다.

TCP가 연결 지향 방식이라는 것은 

패킷을 전송하기 위한 논리적 경로를 배정한다는 말이다.

그리고 3-way handshaking 과정은 목적지와 수신지를 확실히 하여 

정확한 전송을 보장하기 위해 세션을 수립하는 과정을 의미한다.

💡 TCP가 이러한 특징을 지니는 이유는 간단명료하다.

→ TCP는 연결형 서비스로 신뢰성을 보장하기 때문.

그렇기에 **TCP는 연속성보다 신뢰성 있는 전송이 중요할 때에 사용하는 프로토콜**이다.

## ✔️ TCP 서버의 특징

-   서버소켓은 연결만을 담당한다.
-   연결 과정에서 반환된 클라이언트 소켓은 데이터의 송수신에 사용된다.
-   서버와 클라이언트는 1:1로 연결된다.
-   스트림 전송으로 전송 데이터의 크기가 무제한이다.
-   패킷에 대한 응답을 해야하기 때문에 (시간 지연, CPU 소모) 성능이 낮다.
-   Streaming 서비스에 불리하다. (손실될 경우 재전송 요청을 하므로)

> ※ 패킷(Packet)이란?  
> → 인터넷 내에서 데이터를 보내기 위한 경로 배정(라우팅)을 효율적으로 하기 위해   
> 데이터를 여러 개의 조각들로 나누어 전송을 하는데,   
> 이때 이 조각을 패킷이라고 한다.

---

## ✔️ UDP (User Datagram Protocol)

> UDP는 **비연결형 프로토콜**이다.  
>   
> ※ 연결을 위해 할당되는 논리적인 경로가 없고, 각각의 패킷은 다른 경로로 전송되며, 독립적인 관계를 지닌다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdd9lCv%2FbtrZoqNIUv7%2Fnxt0VkehYN3Uj8RbxCeh3k%2Fimg.png)

> 인터넷 상에서 서로 정보를 주고받을 때   
> **정보를 보낸다는 신호나 받는다는 신호 절차를 거치지 않고**   
> **보내는 쪽에서 일방적으로 데이터를 전달하는 통신 프로토콜**이다.  
>   
> TCP와는 다르게 연결 설정이 없으며,   
> 혼잡 제어를 하지 않기 때문에 TCP보다 전송 속도가 빠르다.  
>   
> 그러나 데이터 전송에 대한 보장을 하지 않기 때문에 패킷 손실이 발생할 수 있다.

UDP는 데이터를 데이터그램 단위로 처리하는 프로토콜이다.

> ※ 데이터그램이란?  
> → 독립적인 관계를 지니는 패킷이라는 뜻.  
>   
> TCP와 달리 UDP는 비연결형 프로토콜이다.  
> 즉, 연결을 위해 할당되는 논리적인 경로가 없다.

## ✔️ UDP의 특징

1.  비연결형 서비스로 데이터그램 방식을 제공한다.
    -   데이터의 전송 순서가 바뀔 수 있다.
2.  데이터의 수신 여부를 확인하지 않는다.
    -   TCP의 3-way-handshaking과 같은 과정 X
3.  신뢰성이 낮다.
    -   흐름 제어(Flow Control)가 없어서 제대로 전송되었는지, 오류가 없는지 확인할 수 없다.
4.  TCP보다 속도가 빠르다.
5.  1:1 & 1:N & N:N 통신이 가능하다.

(1) UDP는 비연결형 서비스이기 때문에, 

(2) 연결을 설정하고 해제하는 과정이 존재하지 않는다.

서로 다른 경로로 독립적으로 처리함에도 패킷에 순서를 부여하여 재조립을 하거나 

(3) 흐름 제어 또는 혼잡 제어와 같은 기능도 처리하지 않기에 

(4) TCP보다 속도가 빠르며 네트워크 부하가 적다는 장점이 있지만,

신뢰성있는 데이터의 전송을 보장하지는 못한다.

그렇기 때문에 **신뢰성보다는 연속성이 중요한 서비스** 

예를 들면 실시간 서비스(streaming)에 자주 사용된다.

## ✔️ UDP 서버의 특징

-   UDP에는 연결 자체가 없어서(connect 함수 불필요) 서버 소켓과 클라이언트 소켓의 구분이 없다.
-   소켓 대신 IP를 기반으로 데이터를 전송한다.
-   서버와 클라이언트는 1:1, 1:N, N:M 등으로 연결될 수 있다.
-   데이터그램(메세지) 단위로 전송되며 그 크기는 65535바이트로, 크기가 초과하면 잘라서 보낸다.
-   흐름 제어(flow control)가 없어서 패킷이 제대로 전송되었는지, 오류가 없는지 확인할 수 없다.
-   파일 전송과 같은 신뢰성이 필요한 서비스보다 성능이 중요시 되는 경우에 사용된다.

---

## ✔️ 기타

#### 교환 방식

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FBusKT%2FbtrWeeosb7h%2FX5jc3bMI9uQgXhb5GwBHnK%2Fimg.png)

---

## ✔️ 요약

> TCP는 연속성보다 신뢰성 있는 전송이 중요할 때 사용되는 프로토콜이며,   
>   
> UDP는 TCP보다 빠르고 네트워크 부하가 적다는 장점이 있지만   
> 신뢰성 있는 데이터 전송을 보장하지는 않는다.

## ✔️ 그림으로 비교하는 TCP vs UDP

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbAmnlK%2FbtrWcrbaKa6%2FaduwLJUQasCkCwJo8TbsVK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FVL2CP%2FbtrWgg66CB3%2FQZHjy2dDPwBHMgZk6ZpGvk%2Fimg.webp)

---

### 출처

-   [https://dev-coco.tistory.com/161](https://dev-coco.tistory.com/161)
-   [https://mangkyu.tistory.com/15](https://mangkyu.tistory.com/15)
-   [https://cocoon1787.tistory.com/757](https://cocoon1787.tistory.com/757)
-   [https://coding-factory.tistory.com/614](https://coding-factory.tistory.com/614)
-   [https://github.com/JaeYeopHan/Interview\_Question\_for\_Beginner/tree/master/Network#tcp%EC%99%80-udp%EC%9D%98-%EB%B9%84%EA%B5%90](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Network#tcp%EC%99%80-udp%EC%9D%98-%EB%B9%84%EA%B5%90)
-   [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Network/TCP%20(%ED%9D%90%EB%A6%84%EC%A0%9C%EC%96%B4%ED%98%BC%EC%9E%A1%EC%A0%9C%EC%96%B4).md#tcp-%ED%9D%90%EB%A6%84%EC%A0%9C%EC%96%B4%ED%98%BC%EC%9E%A1%EC%A0%9C%EC%96%B4](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Network/TCP%20(%ED%9D%90%EB%A6%84%EC%A0%9C%EC%96%B4%ED%98%BC%EC%9E%A1%EC%A0%9C%EC%96%B4).md#tcp-%ED%9D%90%EB%A6%84%EC%A0%9C%EC%96%B4%ED%98%BC%EC%9E%A1%EC%A0%9C%EC%96%B4)
-   [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Network/UDP.md#20190826%EC%9B%94-bym-udp%EB%9E%80](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Network/UDP.md#20190826%EC%9B%94-bym-udp%EB%9E%80)
-   [https://velog.io/@ahsy92/%EA%B8%B0%EC%88%A0%EB%A9%B4%EC%A0%91-TCP%EC%99%80-UDP](https://velog.io/@ahsy92/%EA%B8%B0%EC%88%A0%EB%A9%B4%EC%A0%91-TCP%EC%99%80-UDP)
-   [https://dev-coco.tistory.com/144](https://dev-coco.tistory.com/144)