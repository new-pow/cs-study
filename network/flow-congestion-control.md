💡 일반적으로 **TCP는 3-way-handshaking과 흐름제어, 혼잡제어를 통해 신뢰성을 보장**한다.

네트워크 통신 과정 도중에는 네트워크 혼잡성 및 receiver의 overload 등의 사유로 

데이터가 손실되거나, 전달 순서가 바뀌는 등의 문제가 발생할 수 있다.

→ 이런 문제를 해결하고, **통신의 신뢰성을 보장하기 위해 TCP/IP에서 사용하는 것이 흐름제어와 혼잡제어**이다.

💡 이같이 흐름제어는 속도를 일치시키는 서비스이다.

→ 수신하는 애플리케이션이 읽는 속도와, 송신자가 전송하는 속도를 같게 한다.

※ TCP 버퍼

더보기

전송 및 수신 전 TCP 세그먼트를 보관하는 곳이다.

송신 측은 버퍼에 TCP 세그먼트를 보관한 후 순차적으로 전송하고, 

수신 측은 도착한 TCP 세그먼트를 애플리케이션이 읽을 때까지 버퍼에 보관한다.

∴ 이 크기가 너무 작으면 손실되는 데이터가 많아진다.

※ TCP 세그먼트란?

\- TCP 세션으로 연결된 양 끝단 간에 서로 교환, 전달되는 데이터 단위.

## 📌 흐름제어 & 혼잡제어란?

> 혼잡 상황이 발생하면 네트워크 자원이 낭비되므로, 혼잡 상황을 최소화 하기 위한 기법이다.

-   흐름 제어 : 송신측과 수신측의 데이터 처리 속도 차이를 해결하기 위한 기법(송신-수신)
    -   즉, 송신측의 데이터 **전송량** 제어

-   혼잡 제어 : 송신측의 데이터 전달과 네트워크 상의 데이터 처리 속도 차이를 해결하기 위한 기법(송신-네트워크)
    -   즉, 송신측의 데이터 **전송 속도** 제어

그럼 이제 자세히 알아보자.

---

## ✔️ 흐름 제어 (Flow Control)

> **송신측**과 **수신측**의 데이터 처리 속도 차이를 해결하기 위한 기법이다.

-   송신측이 수신측보다 빠르면 상관 없지만, 송신측의 속도가 더 빠를 경우 문제가 생긴다.
    -   수신측에서 저장 가능한 용량을 초과해서 송신측에 계속 데이터를 보낼 경우, **초과된 데이터는 손실될** 수 있으며, **손실될 경우 불필요하게 재전송을 하고 응답을 주고받는 과정**이 생길 수 있다.

> 💡 **따라서 Flow Control은  
> receiver가 지나치게 패킷을 많이 받지 않도록(= receiver buffer가 넘치치 않도록)**   
> **조절하는 것이 중요하다.**

그럼 해결 방법은 무엇일까?

대표적으로 Stop and Wati와 Sliding Window 기법이 있다.

이 두 가지를 알아보자.

## 1\. Stop ans Wait 방식

> 매번 패킷을 보내고 난 후 확인 응답(ACK)을 받아야만 다음 패킷을 전송하는 방식이다. (비효율적)  
>   
> ※ 패킷 : 데이터(정보)를 일정 크기로 자른 것. 즉, 데이터의 단위이다.  
> 이 외에도 OSI 각 계층에서 주고 받는 정보의 단위를 모두 패킷이라고도 함.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbmINie%2FbtrY2ogzhra%2FKFIzCD1MgktLBBncqlNWNK%2Fimg.png)

-   매번 전송한 패킷에 대한 **응답(ACK)을 받은 후**에, 그 다음 패킷을 보낸다.
-   일정 시간(Time out) 동안 **ACK이 도착하지 않으면**, 전송에 실패한 것으로 간주하고, **같은 패킷을 한번 더 전송**한다.
-   즉, 될 때까지 주구장창 보내는 방식이다.

🚨 단점

-   한번에 하나의 패킷만 전송 하기 때문에 **비효율적**이다.
-   Time out 시간이 짧게 설정된 경우, 서버에 보낸 ACK이 전송 진행 중인데도, 클라이언트에서는 이를 전송 실패로 간주하고 같은 패킷을 한번 더 보내게 된다.
-   → **이 방식을 개선한 것이 Sliding Window**이다.

## 2\. Sliding Window

> 수신 측에서 **설정한 '윈도우' 크기**만큼   
> 확인 없이(송신 측의 확인 응답 ACK를 받기 전) 세그먼트를 전송할 수 있도록 하는 것이다.  
>   
> 데이터 흐름을 **동적으로** 조절하는 방식이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDSVv1%2FbtrYYo2ie7z%2FROHLYMPQ6WcBnSAXJGVqhk%2Fimg.png)

-   데이터 흐름(전송)을 동적으로 제어하는 기법이다.
    -   송신 버퍼(= 보낼 수 있는 버퍼를 담아두는 공간)의 범위는 수신 측의 여유 버퍼 공간을 반영하여 동적으로 바뀌기 때문.

※ 동작 과정

더보기

1\. 수신측은 송신측에게 자신의 Receive Window Size에 대해 알려준다.

2\. 송신측은 수신측의 Receive Window Size에 자신의 Send Window Size를 맞춘다.

3\. 송신측은 먼저 윈도우에 포함되는 모든 패킷을 전송하고, 

ACK를 받을 때마다(= 전송한 패킷들의 수신을 확인할 때마다) 윈도우를 옆으로 한 칸씩 이동한다.

4\. 패킷을 보내면, 윈도우의 크기가 줄어든다.

5\. ACK를 받으면, 윈도우의 크기가 증가한다.

\- 수신측에서는 **자신이 마지막으로 확인한 패킷의 번호를 ACK로 전달**.

(→ 누적된 정상 데이터 중 가장 마지막 데이터에 대한 승인 번호를 보내주는 **누적 승인 방식**)

\- 따라서 윈도우의 크기가 반드시 1씩 증가하는 것은 아니다.

(위의 그림에선, ACK3 다음에 바로 ACK6을 전달할 수 있음)

(위의 그림에선, ACK2를 받고 윈도우가 2칸 이동하고, ACK3을 받고 1칸 이동하고, ACK6을 받고 3칸 이동한다.)

6\. (마지막에 보내진 바이트 - 마지막에 확인된 바이트 <= 남아있는 공간)

즉, (현재 공중에 떠있는 패킷 수 <= sliding window)

---

## ✔️ 혼잡 제어 (Congestion Control)

> **송신측**의 데이터 전달과 **네트워크**의 데이터 처리 속도 차이를 해결하기 위한 기법이다.

-   **네트워크의 혼잡 상태**가 감지되었을 때, **송신측의 윈도우 크기를 줄이며** 혼잡 상황을 해결하려고 한다.
-   흐름제어가 송신측과 수신측 사이의 전송 속도를 다루는데 반해, **혼잡제어는 호스트와 라우터를 포함한 보다 넓은 관점에서 전송 문제를 다루게 된다.**

그럼 해결 방법은 무엇일까?

AIMD와 Slow Start를 알아보자.

## 1\. AIMD (Additive Increase / Multiplicative Decrease)

> 처음에 패킷을 하나씩 보내고 이것이 문제 없이 도착하면,  
> window 크기(단위 시간 내에 보내는 패킷의 수)를 1씩 증가시켜가며 전송하는 방법이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcoHgqY%2FbtrYUUglgOs%2FsKJzTyMcJrLBv1BE9ANPek%2Fimg.png)

※ 혼잡 윈도우

더보기

송신 측이 네트워크 상황을 고려해서 정한 윈도우 크기.

-   중간에 데이터가 유실되거나 응답이 오지 않는 등 혼잡 상태가 감지되면, 혼잡 윈도우 크기를 **반으로 줄인다.**
-   공평한 방식으로, 여러 호스트가 한 네트워크를 공유하고 있으면 나중에 진입하는 쪽이 처음에는 불리하지만, 시간이 흐르면 (윈도우의 크기가)평형 상태로 수렴하게 되는 특징이 있다.

🚨 단점

-   네트워크 대역이 펑펑 남아도는 상황에서도 **윈도우 크기를 너무 조금씩 늘리면서 접근**한다는 문제점이 있다.
-   **네트워크가 혼잡해지는 상황을 미리 감지하지 못한다**는 문제점이 있다.
-   즉, 네트워크가 혼잡해지고 나서야 대역폭을 줄이는 방식이다.

## 2\. Slow Start

> 윈도우 크기를 증가할 때는 **지수적으로 증가**시키다가,   
> 혼잡이 감지되면 윈도우 크기를 **1로 줄여버리는** 방식이다.  
>   
> → AIMD에 비해 윈도우 크기를 **빠르게** 키울 수 있음.

-   윈도우 크기가 처음에는 조금 느리게 증가하지만, 시간이 지날수록 윈도우의 크기가 빠르게 증가한다는 장점이 있다.

🚨 이러한 AIMD, Slow Start를 사용하면서 네트워크의 혼잡이 자주 발생하면, 

윈도우의 크기가 크게 감소하고, 네트워크의 전송률이 배우 떨어진다.

∴ TCP에는 **패킷을 재전송하는 기법**들이 존재한다. (혼잡제어 기법의 일종임)

패킷을 재전송하는 2가지 기법을 더 알아보자.

## 3\. Fast Retransmit (빠른 재전송)

> 패킷을 받는 쪽에서 먼저 도착해야 할 패킷이 도착하지 않고 다음 패킷이 도착한 경우에도 ACK 패킷을 보낸다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FUfDXK%2FbtrY4mJFhGZ%2F1226OvjWAAmalFblDB0MJ0%2Fimg.png)

그림 설명 (내 뇌피셜이라 틀렸으면 말해주세요)

-   Sender가 0번 패킷을 보낼 때, Receiver는 응답 ACK1 보냄.(0번 받았으니까 1번 보내줘)
-   Sender가 1을 보낼 때, Receiver는 ACK2 (1번 받았으니까 2번 보내줘)
-   Sender가 2를 보냈는데 중간에 오류생겨서 못보내고 3이 먼저 도착함.
-   이때 3을 받은 Receiver는 ACK2(1번 받았으니까 2번 보내줘)
-   Sender는 계속 그 다음 4을 보냄. Receiver는 ACK2 (1번 받았으니까 2번 보내줘)
-   Sender는 중복 ACK2를 3개 받았으니 이때 감지하고 , 문제가 된 2번 패킷을 즉시 재전송해줌.

💡  이렇게 송신자가 3개 이상의 중복된 ACK를 받는 경우, 바로 패킷을 재전송해준다.

**이런 현상이 일어나면 혼잡 현상이 발생한 것이므로 윈도우 크기를 줄인다**.

## 4\. Fast Recovery (빠른 회복)

> 혼잡한 상태가 되면 window size를 1로 줄이지 않고, 반으로 줄이고 선형 증가 시키는 방법이다.

이 기법까지 적용하면, 혼잡 상황을 겪고 난 후에는 AIMD와 같은 방식으로 동작한다.

---

### 출처

-   컴퓨터 네트워킹 하향식 접근 제 7판
-   [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Network/TCP%20(%ED%9D%90%EB%A6%84%EC%A0%9C%EC%96%B4%ED%98%BC%EC%9E%A1%EC%A0%9C%EC%96%B4).md#tcp-%ED%9D%90%EB%A6%84%EC%A0%9C%EC%96%B4%ED%98%BC%EC%9E%A1%EC%A0%9C%EC%96%B4](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Network/TCP%20(%ED%9D%90%EB%A6%84%EC%A0%9C%EC%96%B4%ED%98%BC%EC%9E%A1%EC%A0%9C%EC%96%B4).md#tcp-%ED%9D%90%EB%A6%84%EC%A0%9C%EC%96%B4%ED%98%BC%EC%9E%A1%EC%A0%9C%EC%96%B4)
-   [https://junghyun100.github.io/TCP-%EC%8B%A0%EB%A2%B0%EC%84%B1-%EB%B3%B4%EC%9E%A5/](https://junghyun100.github.io/TCP-%EC%8B%A0%EB%A2%B0%EC%84%B1-%EB%B3%B4%EC%9E%A5/)
-   [https://inuplace.tistory.com/1081](https://inuplace.tistory.com/1081)
-   [http://www.ktword.co.kr/test/view/view.php?m\_temp1=5611](http://www.ktword.co.kr/test/view/view.php?m_temp1=5611)
-   [https://evan-moon.github.io/2019/11/26/tcp-congestion-control/](https://evan-moon.github.io/2019/11/26/tcp-congestion-control/)