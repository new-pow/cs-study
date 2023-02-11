# 운영체제 IPC

Last edited time: January 30, 2023 10:36 PM
✨ today i learn: https://www.notion.so/2023-01-30-til-829a322f27f340eca5b10cc147935200
분류: Computer Science
상태: not to do

January 30, 2023

---

# Inner Process Communication  프로세스간 통신 IPC

- 독립된 프로세스 간 통신을 뜻한다.

```mermaid
flowchart LR

A[Process A] -->|데이터|B[Process B]
B --> |데이터|A
```

- 일반적으로 1개의 프로그램은 1개 프로세스이나, 서버 프로그래밍을 하는 경우 프로그램이 여러 개의 프로세스를 형성하는 것을 구현할 수 있다.
    - 프로세스 간 통신이 이루어져야지만 적절하게 프로그램이 작동한다.
- 프로세스간 통신은 곧 프로세스간 데이터를 송수신하여 메모리를 공유하는 것을 뜻한다.
    
    ![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F3cea328d-3171-4887-baf1-adea148fa0cd%2FUntitled.png?id=d0b9c8f8-df9d-4c1e-a772-2742b6a284ad&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)
    
- Process 에게는 공간이 **완전히 독립적**으로 주어진다. **안정성!**
    - 메모리 공간에 대해서 다른 프로세스가 접근하지 못하도록 접근을 차단을 **OS(커널)가 보장한다.** == 외부 접근 차단
    - 만약 이게 안된다면, 외부에서 의도적으로 데이터를 변경해 버릴 수 있다. 정말 외부적인 조건을 제외하고는 절대 불가하다.
- 

## IPC 방법1. 메시지 전달 *****Message Passing*****

|  | 메일 슬롯 | 이름없는 파이프 | 이름있는 파이프 |
| --- | --- | --- | --- |
| 방향성 | 단방향, 브로드캐스팅 | 단방향 | 양방향 |
| 통신범위 | 제한 없음 | 외부 컴퓨터 X
부모 자식 프로세스 | 제한 없음 |

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F57502743-ad2c-4f19-befd-4e727af568d2%2FUntitled.png?id=4cdcac61-63d3-4d07-a312-030f3cfb74eb&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

- 커널 메모리 영역에 메시지 전달을 위한 채널을 만들어서 협력하는 프로세스들 사이에 메시지 형태로 정보를 Send/Receive 하는 방법이다.
- OS가 메모리에 일종의 우편함을 만들어준다. 주소를 가졌다.
    - Sender 프로세스는 해당 주소를 통해 데이터를 전송한다.
    - Receiver 프로세스는 데이터가 우체통에 있으면 가져간다.
- 커널을 경유하여 메시지를 송/수신자끼리 주고 받으며, 커널에서는 데이터를 버퍼링한다.
- 커널에서 데이터의 주고 받는 것을 컨트롤할 수 있어 별도의 동기화 로직이 없어도 된다.
- 커널을 통해서 데이터를 주고 받기 때문에 `Shared Memory` 모델보다 느리다.

### 특성

- 단방향이다. Sender는 데이터를 보낼 수만있고 받을 수는 없다.
- 동일한 주소를 부여할 수 있다.
    - Sender가 보내면 한번에 도착하도록 보낼 수 있다.
    - Broadcast

## IPC 방법2. 이름 없는 파이프 (익명 PIPE)

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fa6c35eb1-8ce9-4778-9877-5378e66408be%2FUntitled.png?id=c3bff72e-9483-4bd2-9eb7-879e671dbb5d&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

- 파이프와 입구, 출구의 정보를 가지고 데이터를 주고 받는다.
- 자식 프로세스가 있을 때 부모 프로세스의 파이프를 상속하여 부모-자식 간 데이터 소통이 편하다.
- 두 개의 프로세스를 파이프로 연결하여 하나의 프로세스는 데이터를 쓰기만 하고 다른 프로세스는 데이터를 읽기만 하며 데이터를 통신한다.
    - 반이중 통신 (Half-Duplex)
- 1:1 통신이면서 한 쪽 방향으로만 데이터가 이동한다.
- 주로 **부모-자식 간의 단방향 통신**으로 사용된다.
- 용량 제한이 있기 때문에 파이프가 가득 차면 더 이상 쓸 수 없다.
- 한 쪽 프로세스는 단지 읽기만 하고 다른 프로세스는 단지 쓰기만 하는 단순한 데이터 흐름에 적합하다.

## IPC 방법3. 이름 있는 파이프 (Named PIPE == FIFO)

![](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F65cc4693-3617-4f60-a052-7b4633952087%2FUntitled.png?id=63c78a1b-4b96-44fb-b084-2c9929077ff3&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

- 파이프가 서버와 서버 외부에 연결이 되어있다.
    - (그림은 추상화되어 설명한 것)
- 부모 프로세스와는 무관하게 전혀 다른 모든 프로세스들 사이에서 통신이 가능하다.
    - 프로세스 통신을 위해 이름이 있는 파일을 사용하기 때문

### 단점

- Named PIPE도 읽기/쓰기가 동시에 가능하지 않으며, read-only, write-only만 가능
    - 하지만 통신선로가 파일로 존재하므로 하나를 읽기 전용으로 열고 다른 하나를 쓰기전용으로 영어서 이러한 read/write문제를 해결가능
- 호스트 영역의 서버 클라이언트 간에 이중 통신을 위해서는 결국 두개의 FIFO파일이 필요하게 됩니다.

## IPC 방법4. 공유 메모리 Shared Memory

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F4f3ef4bd-aa51-4f1d-a6ef-86b85c0dd2f2%2FUntitled.png?id=a24b9af7-4b35-4369-9eb8-e835ae705fdc&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

### 공유 메모리 모델 특징

- 두 개 이상의 프로세스들이 주소 공간의 일부를 공유하여, 읽기-쓰기를 통해 통신을 수행한다.
- 프로세스가 공유 메모리 할당을 커널에 요청하면, 커널은 해당 프로세스에 메모리 공간을 할당해 주게 되고, 이후 어떤 프로세스건 해당 메모리 영역에 접근할 수 있다. 공유 메모리가 설정되면, 그 이후의 통신은 커널의 관여 없이 진행이 가능하다.

### 장점

- 커널 관여 없이 메모리에 직접 접근하므로 IPC 속도가 빠르다.
- 프로그램 레벨에서 통신 기능을 제공, 자유로운 통신이 가능하다.

### 단점

- 데이터를 읽어야 하는 시점을 알 수 없어 별도의 동기화 기술이 필요하다.
- 이 동기화 기술로 메모리 업데이트를 알리고 프로세스 하나가 접근하는 동안 다른 프로세스를 막는 매커니즘을 구현하는 것이 번거롭다. == 수동 동기화

## IPC 방법5. Message Queue

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fbf72a653-7879-46cf-97ad-54ce2d2f11d6%2FUntitled.png?id=bf33e8c7-5068-4b4a-9ae4-dc1f8dfafd7f&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

- Queue(큐)는 선입선출의 자료구조를 가지는 통신설비로 커널에서 관리
- 입출력 방식으로 보자면 위의 Named PIPE와 동일
- 위의 파이프가 스트림 기반으로 동작한다면, 메시지 큐는 메시지 (또는 패킷) 단위로 동작한다.
    - `Name PIPE`가 데이터의 흐름
    - `메시지 큐`는 ****메모리 공간

### 장점

- **메시지 큐에 쓸 데이터에 번호를 붙임**으로써 여러 개의 프로세스가 동시에 데이터를 쉽게 다룰 수 있다.
- **양방향 통신이 가능**하며, 메시지 형태는 사용자가 정의하여 사용할 수 있다.
- 부모/자식 관계가 아니더라도, 어느 프로세스 간의 데이터 송수신이 가능하다는 장점이 있다.
- 비동기 방식이기에 방대한 처리량이 있다면 큐에 넣은 후 나중에 처리할 수 있다.

### 단점

- 데이터가 많이 쌓일 수록 추가적인 메모리 자원이 필요하며, 큐에 데이터를 넣고 나오는 과정에서 오버헤드가 발생할 수 있다.

## IPC 방법6. Socket

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F7a0c88b8-6ffa-4d32-9c00-176a97578974%2FUntitled.png?id=1d47c82b-e1b3-4fd5-a666-4355b958edb0&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

- `socke`t은 네트워크 상에서 통신하기 위한 종단점으로 추상화된 개념
- 소켓 통신은 흔히 네트워크 통신 기법으로 많이 사용되는 방법으로, 양쪽 PC에서 각각 임의의 포트를 정하고 해당 포트 간의 대화를 통해 데이터를 주고 받는 방식
- 소켓이 네트워크 기능을 담고 있다 보니 네트워크 기능을 이용해 IPC로도 사용할 수 있다.
    - 소켓을 한 PC 내 두 개의 프로세스 간 통신 기법으로도 사용이 가능
    - 기존의 네트워크 상에서 소켓 통신과 달라지는 점은 sock_addr_in 구조체를 sock_addr_un으로 변경하고, 속성을 AF_INET에 대해 AF_UNIX로 변경한 뒤 소켓 통신을 하기 위한 파일 경로가 필요하다고 한다.

### **특징**

- 네트워크 소켓을 이용하여 Client - Server 구조로 데이터 통신을 하며, 원격에서 프로세스 간 데이터를 공유할 때 사용한다.
- 프로세스는 포트 번호를 이용하여 통신하려는 상대 프로세스의 소켓을 찾아간다.
- 포트의 도움으로, 다른 IPC와 달리 **프로세스의 위치에 독립적**이며, Machine Boundary와 관계가 없기 때문에 Local 또는 Remote로 사용할 수 있다. **다른 IPC는 모두 local에서만 사용할 수 있다.**

### 방법

- 서버 단에서는 `bind` 주소할당, `listen` 통신요청 대기, `accept` 통신 수락을 진행하여 소켓 연결을 위한 준비를 하고
- 클라이언트 단에서는 `connect` 통신 요청를 통해 서버에 요청하고 연결이 수립된 후, `socket`에 `send`함으로써 데이터를 주고 받는다.

### 장점

- 범용적인 IPC로서 **양방향 통신**이 가능하다.
- **패킷 단위**로 주고 받음으로써 직관적으로 이해하기 쉬운 코드를 만들 수 있다.

### 단점

- 하지만 Internet UDP와는 달리 경로를 지정할 수는 없다.

---

- 참고
    - [https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=kbh3983&logNo=220788898350](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=kbh3983&logNo=220788898350)
    - [https://jwprogramming.tistory.com/54](https://jwprogramming.tistory.com/54)
    - [https://hidemasa.tistory.com/49](https://hidemasa.tistory.com/49)
    - [https://ko.wikipedia.org/wiki/프로세스_간_통신](https://ko.wikipedia.org/wiki/%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4_%EA%B0%84_%ED%86%B5%EC%8B%A0)