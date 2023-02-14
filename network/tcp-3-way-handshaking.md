> 💡 연결을 성립하고 해제하는 과정을 말한다.

## 3 way-handshake란? : 연결을 설정하는 과정

> TCP 네트워크에서 통신하는 장치가 서로 연결이 잘 되었는지 확인하는 방법 (연결 성립)

송신자와 수신자는 총 3번에 걸쳐 데이터를 주고 받으며, 

**통신이 가능한 상태인지 확인**한다.

TCP는 정확한 전송을 보장해야 한다.

따라서 T**CP/IP프로토콜을 이용해 통신하기에 앞서,**

**논리적인 접속을 성립하기 위해 3** **way handshake 과정을 진행**한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fv3lTw%2FbtrWdgtmDz2%2FjdXJkKNWEaqlFUiViUkv61%2Fimg.png)

-   Client → Server : TCP SYN
-   Server → Client : TCP SYN + ACK
-   Clinet → Server : TCP ACK

> ※ 참고  
> \- SYN : Synchronize Sequence Numbers  
> \- ACK : Acknowledgment (승인)

이러한 절차는 TCP 접속을 성공적으로 성립하기 위해 반드시 필요하다.

## TCP의 3-way Handshaking 역할

\- 양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장하고, 

실제로 데이터 전달이 시작하기 전에 한쪽이 다른 쪽이 준비되었다는 것을 알 수 있도록 한다.

\- 양쪽 모두 상대편에 대한 초기 순차일련번호를 얻을 수 있도록 한다.

## TCP의 3-way Handshaking의 과정

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbTZdTp%2FbtrWg031U29%2Fg5UJQVNi7QxkM9yhGv12v1%2Fimg.png)

#### Step 1 (Client → Server : SYN)

> \- 클라이언트가 서버에게, 연결을 요청하는 메시지 SYN을 보낸다.  
> \- 최초로 데이터를 전송할 때, Sequence Number를 임의의 숫자(난수)로 지정하고,   
> SYN 비트를 1로 해서 보낸다.

> 💡 요약  
> Client는 Server에 접속 요청 메세지(SYN)을 전송하고, SYN\_SEND 상태가 된다.

#### Step 2 (Server → Client : SYN + ACK)

> \- 서버가 클라이언트의 요청을 수락했으며(ACK),   
> 클라이언트의 포트도 열어달라는 메시지를 보낸다.(SYN)  
> \- 이 때, ACK 필드를 (Sequence Number + 1)로 지정하고   
> SYN과 ACK의 비트를 1로 설정한다.

> 💡 요약  
> Server는 SYN 요청을 받고 Client에 요청을 수락(SYN + ACK)하고,   
> SYN\_RECIEVED 상태가 된다.

#### Step 3 (Client → Server : ACK)

> \- 클라이언트에서 서버가 요청을 수락했음을 확인하는 응답 ACK를 보낸다.  
> \- 이 때, 보내려는 데이터가 있으면 이 단계에서 전송을 수행할 수 있다.

> 💡 요약  
> Client는 Server에게 수락 확인(ACK)를 보내고, Server는 ESTACLISHED 상태가 된다.

이렇게 3번의 통신이 완료되면, 연결이 성립한다.

(3번이라 3 way handshake인 것)

---

## 4 way-handshake란? : 연결을 해제하는 과정

> TCP 네트워크에서 통신하는 장치의 연결을 해제하는 방법

송신자와 수신자는 총 4번에 걸쳐 데이터를 주고 받으며 **연결을 끊는다.**

즉, 연결 성립 후, 모든 통신이 끝났다면 해제하야 한다.

3-Way handshake는 TCP의 연결을 초기화 할 때 사용한다면, 

4-Way handshake는 세션을 종료하기 위해 수행되는 절차이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJSVaw%2FbtrWeeBQbxq%2Fh03nHowdVPstIJkh1OPucK%2Fimg.png)

## TCP의 4-way Handshaking의 과정

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbjDy7F%2FbtrWca8fSnY%2F9YBu54Gz7YZPKdylhZ2XHK%2Fimg.png)

#### Step 1 (Client → Server : FIN)

> \- 클라이언트가 서버에게 연결을 종료하겠다는 FIN 플래그 전송  
> \- 서버로부터 FIN 응답을 받을 때 까지는 연결을 close 하지 못함

#### Step 2 (Server → Client : ACK)

> \- 서버는 FIN을 받고, 확인했다는 ACK를 클라이언트에게 보낸다.  
> \- 이 때, 모든 데이터를 보내기 위해 **CLOSE\_WAIT** 상태가 된다.

#### Step 3 (Server → Client : FIN)

> \- 서버가 통신이 끝났으면, 연결 종료 요청에 응한다는 의미로 FIN을 보냄

#### Step 4 (Client → Server : ACK)

> \- 클라이언트는 FIN을 받고, 확인했다는 ACK를 서버에게 보낸다.  
> \- 이 때, 아직 서버로부터 받지 못한 데이터가 있을 수 있으므로 TIME\_WAIT를 통해 기다린다.

> ※ TIME\_WAIT란?  
> \- 클라이언트가 서버로부터 FIN 응답을 받고 난 이후에도,   
> 바로 연결을 종료하지 않고 일정시간 동안 기다리는 상태.

> <TIME\_WAIT 부가 설명>  
> ❓ 만약 "Server에서 FIN을 전송하기 전에,   
> 전송하고 있던 패킷이 Routing 지연이나 패킷 유실로 인한 재전송 등으로 인해   
> FIN 패킷보다 늦게 도착하는 상황"이 발생한다면?  
>   
> → Cilent에서 세션을 종료시킨 후 뒤늦게 도착하는 패킷이 있다면,   
> 이 패킷은 Drop되고 데이터는 유실될 것이다.  
> 이러한 현상에 대비하여 Client는 Server로부터 FIN을 수신하더라도  
> 일정시간(디폴트 240초) 동안 세션을 남겨놓고 잉여 패킷을 기다리는 과정을   
> 거치게 되는데 이 과정을 "TIME\_WAIT"이라고 한다.

-   서버는 ACK를 받을 이후 소켓을 닫는다. (Closed)
-   TIME\_WAIT 시간이 끝나면 클라이언트도 닫는다.(Closed)

이렇게 4번의 통신이 완료되면, 연결이 해제된다.

---

### 출처

-   [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Network/TCP%203%20way%20handshake%20%26%204%20way%20handshake.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Network/TCP%203%20way%20handshake%20%26%204%20way%20handshake.md)
-   [https://dev-coco.tistory.com/161](https://dev-coco.tistory.com/161)
-   [https://blex.me/@baealex/%EC%B7%A8%EC%A4%80%EC%83%9D%EC%9D%B4-%EC%83%9D%EA%B0%81%ED%95%98%EB%8A%94-%EA%B0%9C%EB%B0%9C%EC%9E%90-%EA%B8%B0%EC%88%A0%EB%A9%B4%EC%A0%91-%EC%A4%80%EB%B9%84#tcp-3-way-handshake](https://blex.me/@baealex/%EC%B7%A8%EC%A4%80%EC%83%9D%EC%9D%B4-%EC%83%9D%EA%B0%81%ED%95%98%EB%8A%94-%EA%B0%9C%EB%B0%9C%EC%9E%90-%EA%B8%B0%EC%88%A0%EB%A9%B4%EC%A0%91-%EC%A4%80%EB%B9%84#tcp-3-way-handshake)
-   [https://mindnet.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-22%ED%8E%B8-TCP-3-WayHandshake-4-WayHandshake](https://mindnet.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-22%ED%8E%B8-TCP-3-WayHandshake-4-WayHandshake)
-   [https://gmlwjd9405.github.io/2018/09/19/tcp-connection.html](https://gmlwjd9405.github.io/2018/09/19/tcp-connection.html)