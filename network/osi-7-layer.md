## OSI 7 계층이란? 

> 네트워크에서 통신이 일어나는 과정을 7단계로 나눈 것을 말한다.

## 7 계층은 왜 나눌까? 

> 통신이 일어나는 과정을 단계별로 알 수 있고,  
> 네트워크 관리자는 어떤 문제의 원인이 어디에 있는지 범위를 좁힐 수 있다.  
>   
> 특정한 곳에 이상이 생기면 다른 단계를 건들이지 않고도 그 단계만 수정할 수 있기 때문

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbg8sgD%2FbtrVzJCMnVj%2FgIo1Y8psHuQwl31nSSrUck%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAJzad%2FbtrVCf8fhiH%2FuJrxxpB19AK3dLjcBEuyC0%2Fimg.png)

---

## 7계층 – 응용 계층(Application)

> HTTP, FTP, DNS 등

> 디핑 소스 비유를 확장하면, 응용 계층은 가장 위에 있다.  
> 사용자에게 보이는 부분이다.  
> OSI 모형에서는  "최종 사용자에게 가장 가까운" 계층이다.  
>   
> 7계층에서 작동하는 응용프로그램은 **사용자와 직접적으로 상호작용**한다.  
>   
> 최종 목적지로, 응용 프로세스와 직접 관계하여 일반적인 응용 서비스를 수행한다.  
> 사용자 인터페이스, 전자우편, 데이터베이스 관리 등의 서비스를 제공한다.  
>   
> 구글 크롬(Google Chrome), 파이어폭스(Firefox), 사파리(Safari) 등 웹 브라우저와  
> 스카이프(Skype), 아웃룩(Outlook), 오피스(Office) 등의 응용 프로그램이 대표적이다.

\- 사용자와 가장 밀접한 계층, 인터페이스(Interface) 역할

\- 응용 프로세스 간의 정보 교환 담당 / 전송 단위 : Message

\- EX : 전자 메일, 인터넷, 동영상 플레이어 등의 Applicasation

**: User Interface 를 제공하는 계층**

---

## 6계층 – 표현 계층(Presentation)

> JPEG, MPEG 등

> 표현 계층은 응용 계층의 데이터 표현에서 독립적인 부분을 나타낸다.  
> 일반적으로 응용프로그램 형식을 준비 또는 네트워크 형식으로 변환하거나,   
> 네트워크 형식을 응용프로그램 형식으로 변환하는 것을 나타낸다.  
>   
> 다시 말해 이 계층은 응용프로그램이나 네트워크를 위해 데이터를 “**표현**”하는 것이다.  
>   
> 대표적인 예로는 데이터를 안전하게 전송하기 위해 암호화, 복호화하는 것인데,  
> 이 작업이 바로 6계층에서 처리된다.  
>   
> 데이터 표현에 대한 독립성을 제공하고 암호화하는 역할을 담당한다.  
> 파일 인코딩, 명령어를 포장, 압축, 암호화한다.

\- 데이터 표현에 차이가 있는 응용처리에서의 제어구조를 제공

※ 데이터 표현에 차이 : ASCII, JPEG, MPEG 등의 번역

\- 전송하는 데이터의 인코딩, 디코딩, 암호화, 코드 변환 등을 수행 / 전송 단위 : Message

**: 데이터의 변환 작업을 하는 계층**

---

## 5계층 – 세션 계층(Session)

> API, Socket

> 데이터가 통신하기 위한 논리적 연결을 담당한다.  
> 통신을 하기위한 대문이라고 보면 된다.  
> TCP/IP 세션을 만들고 없애는 책임을 지니고 있다.  
>   
> 2대의 기기, 컴퓨터 또는 서버 간에 “대화”가 필요하면 세션(session)을 만들어야 하는데  
> 이 작업이 여기서 처리된다.

\- 통신장치 간 상호작용 및 동기화를 제공

\- 연결 세션에서 데이터 교환,  에러 발생 시 복구 관리 => 논리적 연결 담당 / 전송 단위 : Message

\- 4계층 장비 : NetBIOS (세션 내 연결관리 및 에러감지, 복구 수행), SSH, Appletalk  (Port는 4~5계층 경계 모호)  
**: 응용 프로그램 간의 연결을 지원해주는 계층**

---

## 4계층 – 전송 계층(Transport)

> TCP, UDP

-   TCP : 신뢰성, 연결지향적
-   UDP : 비신뢰성, 비연결성, 실시간

> 최종 시스템 및 호스트 간의 데이터 전송 조율을 담당한다.  
> 보낼 데이터의 용량과 속도, 목적지 등을 처리한다.  
>   
> 전송 계층의 예 중에서 가장 잘 알려진 것이 전송 제어 프로토콜(**TCP**)이다.  
> TCP는 인터넷 프로토콜(IP) 위에 구축되는데 흔히 TCP/IP로 알려져 있다.  
> 기기의 IP 주소가 여기서 작동한다.  
>   
> TCP와 UDP 프로토콜을 통해 통신을 활성화한다.  
> 보통 TCP프로토콜을 이용하며, 포트를 열어서 응용프로그램들이 전송을 할 수 있게 한다.  
>   
> 만약 데이터가 왔다면 4계층에서 해당 데이터를 하나로 합쳐서 5계층에 던져 준다.

\- 종단 간(End-to-End)에 신뢰성 있고 정확한 데이터 전송을 담당 / 전송 단위 : Segment

\- 4계층에서 전송 되는 단위 => 세그먼트(Segment), 종단 간의 에러 복구와 흐름 제어 담당  ex) **TCP/UDP**

\- 4계층 장비 : L4 스위치 (3계층 트래픽 분석, 서비스 종류 구분)  
**: 서비스를 구분하고 데이터의 전송 방식을 담당하는 계층 (TCP/UDP)**

---

## 3계층 – 네트워크 계층(Network)

> 라우터, IP

> **데이터를 목적지까지 가장 안전하고 빠르게 전달하는 기능(라우팅)을 담당**한다.  
> 라우터를 통해 이동할 경로를 선택하여 IP 주소를 지정하고, 해당 경로에 따라 패킷을 전달해준다.  
>   
> 라우팅, 흐름 제어, 세그멘테이션, 오류 제어, 인터네트워킹등을 수행한다.

\- 중계 노드를 통하여 전송하는 경우, 어떻게 중계할 것인가를 규정  / 전송 단위 : Packet

\- 데이터를 목적지까지 가장 안전하고 빠르게 전달 => 라우팅

\- 3계층 장비 : 라우터, L3 스위치

**: 네트워크를 논리적으로 구분하고 연결하는 계층 - 논리적 주소 사용**

---

## 2계층 – 데이터 링크 계층(Data Link)

> 브릿지, 스위치 등

> 물리계층을 통해 송수신되는 정보의   
> **오류와 흐름을 관리하여 안전한 정보의 전달을 수행할 수 있도록 도와주는 역할**을 한다.  
>   
> 따라서 **통신에서의 오류도 찾아주고 재전송도하는 기능을 가지고 있는 것**이다.  
>   
> 여기에는 2개의 부계층도 존재한다.  
> 하나는 매체 접근 제어(MAC) 계층이고,  
> 다른 하나는 논리적 연결 제어(LLC) 계층이다.  
> → 네트워킹 세계에서 대부분 스위치는 2계층에서 작동한다.  
>   
> 프레임에 Mac 주소를 부여하고 에러검출, 재전송, 흐름제어를 진행한다.

\- 물리적인 연결을 통하여 인접한 두 장치간의 신뢰성 있는 정보 전송을 담당   / 전송 단위 : Frame

\- 정보의 오류와 흐름을 관리. 안정된 정보 전달 　　 　　 　　

\- 2계층 장비 : 브리지, 스위치

**: 물리적 매체에 패킷 데이터를 실어 보내는 계층 - 환경에 맞는 다양한 통신 프로토콜 지원**

---

## 1계층 – 물리 계층(Physical)

> 리피터, 케이블, 허브 등

> 이 계층에서는 주로 전기적, 기계적, 기능적인 특성을 이용해서  
> **통신 케이블로 데이터를 전송**하게 된다.  
>   
> 이 계층에서 사용되는 **통신 단위는 비트**이며, 이것은 **1과 0으로 나타내어지는**   
> 즉, **전기적으로 ON, OFF 상태**라고 생각하면 된다.  
>   
> 이 계층에서는 단지 데이터를 전달할 뿐   
> 전송하려는 데이터가 무엇인지, 어떤 에러가 있는지 등에는 전혀 신경을 쓰지 않는다.

\- 전기적, 기계적 특성을 이용하여, 통신 케이블로 전기적 신호(에너지)를 전송   / 전송 단위 : bit

\- 단지 데이터 전달 역할만을 하고, 알고리즘, 오류 제어 기능 존재 X  　　 

\- 1계층 장비 : 리피터, 허브, 케이블

**: 신호로 변환하여 전송하는 계층**

---

# TCP/IP란?

> 데이터가 의도된 목적지에 닿을 수 있도록 보장해주는 통신 규약이다.  
> TCP와 IP 두가지의 프로토콜로 이루어져 있다.

## TCP(Transmission Control Protocol)

> 두 호스트가 교환하는 데이터와 승인 메세지의 형식을 정의하여,   
> 서버와 클라이언트 간의 데이터를 신뢰성있게 전달하기 위해 만들어진 규약이다.  
>   
> 컴퓨터와 컴퓨터를 이어주는 네트워크는 네트워크 선로를 통해 전달되는데,  
> 이 선로는 광케이블일수도, 구리선일수도, 인공위성 일수도 있다.  
> 어떤 선로인지에 따라 데이터를 전달하는 속도와 손실되는 데이터의 양이 달라지는데,  
> 이는 데이터를 전달하는 과정에서 그 순서가 의도하지 않게 뒤바뀌거나 손실이 되어 전달될 수 있음을 뜻한다.  
>   
> TCP는 데이터 패킷에 일련의 번호를 부여함으로써,  
> 데이터 손실을 찾아내서 교정하고, 순서를 재조합하여 클라이언트에게 전달할 수 있게 해준다.  
>   
> TCP의 장점은 복잡해서 신뢰성이 높다는 점이다.

## IP(Internet Protocol)

> 컴퓨터와 컴퓨터간에 데이터를 전송하기 위해서, 각 컴퓨터의 주소가 필요하다.  
>   
> Internet Protocol은 4바이트로 이루어진 컴퓨터의 주소이며,   
> 192.168.9.255와 같이 3개의 마침표로 나뉘어진 숫자로 표시된다.  
>   
> IP는 TCP와는 달리 데이터의 재조합이나 손실여부 확인이 불가능하며,  
> 단지 데이터를 전달하는 역할만을 담당한다.  
>   
> ※ 참고로 IP주소는 하드웨어 고유의 식별번호인 MAC주소와 다르게  
> 임시적으로 다른 주체(통신사)에게 받는 주소이므로, 바뀔수 있다.

---

## TCP/IP

> IP기반에 TCP가 사용되서 이렇게 불린다고 한다.  
> TCP가 데이터의 추적을, IP가 배달을 처리한다고 보면 된다

## TCP/IP Protocol (4계층)

> TCP/IP는 현재의 인터넷에서 컴퓨터들이 서로 정보를 주고받는데 쓰이는 통신규약 (프로토콜)의 모음이다.  
> 하드웨어, 운영체제, 접속매체에 관계없이 동작할 수 있는 개방성을 가진다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcen7tl%2FbtrVALNwH5x%2FzDmFm2AsKmumnXkqPn9GI0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAJzad%2FbtrVCf8fhiH%2FuJrxxpB19AK3dLjcBEuyC0%2Fimg.png)

---

## 4계층 - Application Layer  

> **프로그램(브라우저)가 직접 인터액트하는 레이어.**  
> **데이터를 처음으로 받는곳.**  
> **HTTP, SMTP등의 프로토콜을 가진다.**

(1) OSI 7 Layer에서 세션계층 , 프레젠테이션계층, 애플리케이션 계층에 해당한다. (5, 6, 7계층)

(2) 응용프로그램들이 네트워크서비스, 메일서비스, 웹서비스 등을 할 수 있도록 표준적인 인터페이스를 제공한다.

\- TCP/IP 기반의 **응용 프로그램**을 구분할 때 사용한다.

\- 프로토콜 : HTTP, FTP, Telnet, DNS, SMTP

---

## 3계층 - Transport Layer

> TCP가 있는 레이어.  
> 포트를 통하여 Application 레이어가 TCP에게 데이터를 전송한다.

> 각각의 포트에 프로토콜을 지정할 수 있다.  
>   
> 예를 들어, HTTP는 80이라는 포트를 사용한다.  
> 이로써, TCP는 어디에서 데이터가 오는지를 정확히 알 수 있다.  
>   
> 포트를 통해 받은 데이터들은 패킷이라는 작은 단위로 쪼개진다.  
> 이 패킷들은 제각각 가장 빨리 전송될 수 있는 인터넷 루트를 찾아 떠난다.  
>   
> 각각의 패킷들은 TCP header에 어떤 순서로 재조합 할지에 관한 정보를 가진다.

(1) OSI 7 Layer에서 전송계층에 해당한다.

(2) 네트워크 양단의 송수신 호스트 사이에서 신뢰성 있는 전송기능을 제공한다.

(3) 시스템의 논리주소와 포트를 가지고 있어서 각 상위 계층의 프로세스를 연결해서 통신한다.

(4) 정확한 패킷의 전송을 보장하는 TCP와 정확한 전송을 보장하지 않는 UDP 프로토 콜을 이용한다.

(5) 데이터의 정확한 전송보다 빠른 속도의 전송이 필요한 멀티미디어 통신에서 UDP 를 사용하면 TCP보다 유용하다.

\- **통신 노드 간의 연결을 제어**하고, 자료의 송수신을 담당

\- 프로토콜 : TCP, UDP

---

## 2계층 - Internet Layer

> 패킷들이 인터넷 레이어에 push된다.   
> IP를 사용하여 데이터의 원천지(origin)와 목적지(destination)에 관한 정보를 첨부한다.

(1) OSI 7 Layer의 네트워크 계층에 해당한다.

(2) 인터넷 계층의 주요 기능은 상위 트랜스포트 계층으로부터 받은 데이터에 

IP패킷 헤더를 붙여 IP패킷을 만들고 이를 전송하는 것이다.

\- 통신 노드 간의 **IP 패킷을 전송**하는 기능 및 라우팅 기능을 담당

\- 프로토콜 : IP, ARP, RARP, ICMP, OSPF

---

## 1계층 - Network Access Layer

> 마지막으로 패킷들은 네트워크 레이어로 전송된다.  
> 알맞은 하드웨어로 데이터가 전달되도록 MAC 주소를 핸들링 하는 것 뿐 아니라,   
> 데이터 패킷을 전기신호로 변환하여 선로를 통하여 전달할 수 있게 준비해준다.

(1) OSI 7 Layer에서 물리계층과 데이터링크 계층에 해당한다.

(2) OS의 네트워크 카드와 디바이스 드라이버 등과 같이 하드웨어적인 요소와 관련되 는 모든 것을 지원하는 계층

(3) 송신측 컴퓨터의 경우

상위 계층으로부터 전달받은 패킷에 물리적인 주소는 MAC 주소 정보를 가지고 있는 헤더를 추가하여 프레임을 만들고, 

프레임을 하위계층인 물리 계층으로 전달한다.

(4) 수신측 컴퓨터의 경우 데이터 링크 계층에서 추가된 헤더를 제거하여 상위 계층인 네트워크 계층으로 전달한다.

\- CSMA/CD, MAC, LAN, X25, 패킷망, 위성 통신, 다이얼 모뎀 등 **전송에 사용**

\- 프로토콜 : Ehternet(이더넷), Token Ring, PPP

---

## 장점

-   open source
-   industry standard
-   scalable
-   interoperable (다른 시스템 사이에서도 전송 가능)

## 쓰임새

> EMAIL(SMTP), HTTP, HTTPS, FTP, TELNET 등  
> 우리에게 친숙한 인터넷 서비스의 대부분이 TCP/IP기반이다.

---

## OSI 모델과 TCP/IP 모델 비교

> \- TCP/IP 프로토콜은 OSI 모델보다 먼저 개발되었다.  
> 그러므로 TCP/IP 프로토콜의 계층은 OSI 모델의 계층과 정확하게 일치하지 않는다.  
>   
> \- 두 계층을 비교할 때,   
> 세션(Session)과 표현(Presentation) 2개의 계층이 TCP/IP 프로토콜 그룹에 없다는 것을 알 수 있다.  
>   
> \- 두 모델 모두 **계층형**이라는 공통점을 가지고 있으며   
> **TCP/IP는 인터넷 개발 이후 계속 표준화된어 신뢰성이 우수**인 반면,   
> OSI 7 Layer는 표준이 된기는 하지만   
> 실제적으로 구현되는 예가 거의 없어 신뢰성이 저하되어있다.  
>   
> \- OSI 7 Layer는 장비 개발과 통신 자체를 어떻게 표준으로 잡을지 사용되는 반면에   
> 실질적인 통신 자체는 TCP/IP 프로토콜을 사용한다.

---

## 📌 요약

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FGWO4e%2FbtrYUS3Mok4%2FtXIMskUdnH2Y3ouofw0dik%2Fimg.jpg)

\[OSI 7계층\]

-   7 계층 (응용 계층) : 사용자와 직접 상호작용하는 응용 프로그램들이 포함된 계층
-   6 계층 (표현 계층) : 데이터의 형식(Format)을 정의하는 계층
-   5 계층 (세션 계층) : 컴퓨터끼리 통신을 하기 위해 세션을 만드는 계층
-   4 계층 (전송 계층) : 최종 수신 프로세스로 데이터의 전송을 담당하는 계층
-   3 계층 (네트워크 계층) : 패킷을 목적지까지 가장 빠른 길로 전송하기 위한 계층
-   2 계층 (데이터링크 계층) : 데이터의 물리적인 전송과 에러 검충, 흐름제어를 담당하는 계층
-   1 계층 (물리 계층) : 데이터를 전기 신호로 바꾸어주는 계층

---

### 출처

-   [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Network/OSI%207%20%EA%B3%84%EC%B8%B5.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Network/OSI%207%20%EA%B3%84%EC%B8%B5.md)
-   [https://articles09.tistory.com/43](https://articles09.tistory.com/43)
-   [https://ryusae.tistory.com/4](https://ryusae.tistory.com/4)
-   [https://velog.io/@rosewwross/TCPIP](https://velog.io/@rosewwross/TCPIP)
-   [https://mangkyu.tistory.com/91](https://mangkyu.tistory.com/91)