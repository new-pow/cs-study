## PCB란?

> PCB(Process Control Block)는 CPU가 프로세스가 여러 개일 때,  
> CPU 스케줄링을 통해 관리하는 것을 말한다.

> ❗ 이때, CPU는 각 프로세스들이 누군지 알아야 관리가 가능하다.  
>   
> → 프로세스들의 특징을 갖고있는 것이 바로 **Process Metadata**이다.

> ※ Metadata (메타데이터)란?  
> : **데이터에 관한 구조화된 데이터**로,  
> 대량의 정보 가운데에서 확인하고자 하는 정보를 효율적으로 찾아내서 이용하기 위해   
> 일정한 규칙에 따라 콘텐츠에 대해 부여되는 데이터이다.

Process Metadata에는 다음과 같은 정보들이 있다.

## PCB에 담기는 프로세스 정보

> PCB는 프로세스 스케줄링 상태, 프로세스 ID 등의 다음과 같은 정보들로 이루어져 있다.

-   Process ID (PID(Process Identification Number)라고도 한다.) : 프로세스 고유 식별 번호
-   Process State(프로세스 상태) : 프로세스의 현재 상태(준비, 실행, 대기 상태)를 기억시킨다.
-   Process Priority(스케줄링 정보) : 프로세스 우선순위 등과 같은 스케줄링 관련 정보를 기억시킨다.
-   CPU Registers : 프로세스의 레지스터 상태를 저장하는 공간 등. CPU 내 범용 레지스터(AX, BX, CX, DX), 데이터 레지스터(SP, BP, SI, DI), 세그먼트 레지스터(CS, DS, ES, SS) 등이 갖고 있는 값을 기억시킨다.
-   Owner(계정 정보) : CPU 사용시간의 정보(Quantum), 각종 스케줄러에 필요한 정보를 기억시킨다.
-   기억장치 관리 정보 : 프로그램이 적재될 기억 장치의 상한치, 하한치, 페이지 테이블 등의 정보를 기억시킨다.
-   입출력 정보 : 프로세스 수행 시 필요한 주변 장치, 파일들의 정보를 기억시킨다.
-   프로그램 카운터(계수기) : 다음에 실행되는 명령어의 주소를 기억시킨다.

이 메타데이터는 프로세스가 생성되면, PCB(Process Control Block)이라는 곳에 저장된다.

## PCB (Process Control Block)

> 운영체제가 프로세스 메타데이터들(중요한 정보)을 저장해 놓는 저장 장소이다.  
> 한 PCB 안에는 한 프로세스의 정보가 담긴다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdLEx8d%2FbtrXgpQRsiP%2FI8JPMqWUtxPkkW5erC1X31%2Fimg.png)

**다시 정리해보면?**

> 프로그램 실행 → 프로세스 생성 → 프로세스 주소 공간에 (코드, 데이터, 스택) 생성   
> → 이 프로세스의 메타데이터들이 PCB에 저장.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FpRQfe%2FbtrXhwnZpjW%2FwKhTjkQNWsyMnNkzEk3y5K%2Fimg.png)

## 그럼 PCB가 왜 필요할까?

> CPU에서는 프로세스의 상태에 따라 교체 작업이 이루어진다.  
> (인터럽트가 발생해서 할당받은 프로세스가 Block 상태가 되고,   
> 다른 프로세스를 running으로 바꿀 때)  
>   
> ❗ 이때, **앞으로 다시 수행할 Block 상태의 프로세스의 상태값을 PCB에 저장해두는 것**이다.

## PCB는 어떻게 관리될까?

> Linked List 방식으로 관리된다.  
>   
> PCB List Head에 PCB들이 생성될 때마다 붙게 된다.  
> 주소값으로 연결이 이루어져 있는 연결리스트이기 때문에 **삽입, 삭제가 용이**하다.  
>   
> 즉, **프로세스가 생성되면 해당 PCB가 생성되고 프로세스 완료시 제거된다.**

✔️ 이렇게 수행 중인 프로세스를 변경할 때, CPU의 레지스터 정보가 변경되는 것을 

**Context Switching**이라고 한다.

---

## Context Switching

> CPU가 이전의 프로세스 상태를 PCB에 보관하고,   
> 또다른 프로세스의 정보를 PCB에 읽어 레지스터에 적재하는 과정이다.  
>   
> 즉, 컨텍스트 스위칭(Context Switching)은 앞서 설명한 PCB를 교환하는 과정을 말한다.  
> 한 프로세스에 할당된 시간이 끝나거나, 인터럽트에 의해 발생한다.  
>   
> ※ 컴퓨터는 많은 프로그램을 동시에 실행하는 것처럼 보이지만,   
> **어떠한 시점에서 실행되고 있는 프로세스는 단 한 개**이며,   
> 다른 프로세스와의 **컨텍스트 스위칭이 아주 빠른 속도로 실행**되기에 **동시 구동처럼 보이는 것**이다.

> ※ 줄글로 풀어보는 스토리텔링  
>   
> **현재 CPU가 현재 실행하고 있는 프로세스의 정보를 '문맥(Context)'**라고 하니,   
> 이를 교환하는 문맥 교환(Context Switching)이라고 정의 내릴 수 있다.  
>   
> 현재 실행 중인 프로세스의 정보들 담고 있는 CPU 레지스터의 내용이,   
> 다음 실행할 프로세스의 정보로 변경되는 것을 의미한다.  
>   
> 즉, 프로세스A를 실행 중이던 CPU가 프로세스B를 실행하기 위해   
> 프로세스A의 정보를 '**어딘가**'에 저장하고,   
> 프로세스B의 정보를  '**어딘가**'로부터 꺼내오는 것을 의미한다.  
>   
> ✔️ **여기서 말하는 '어딘가'가 바로 PCB(Process Control Block)이다.**

## 왜 Context Switching이 필요한가?

(가정)

만약 컴퓨터가 매번 하나의 Task만 처리할 수 있다면?

-   다음 Task를 처리하기 위해서 현재 Task가 끝날 때까지 기다려야 한다.
-   반응속도가 매우 느리고 사용하기 불편하다.

✔️ 이처럼 **다양한 사람들이 동시에 사용하는 것처럼 하기 위해,** 

Context Switching이 필요하게 되었다.

-   컴퓨터 멀티태스킹을 통해 빠른 반응속도로 응답 가능하다.
-   빠르게 Task를 바꾸면서 실행하기에, 사람은 실시간처리가 되는 것처럼 보인다.
-   CPU가 Task를 바꿔가며 실행하기 위해 Context Switching이 필요하게 되었다.

## Context Switching는 언제 발생할까?

> 인터럽트가 발생하거나, 실행 중인 CPU 사용 허가 시간을 모두 소모하거나,   
> 입출력을 위해 대기해야 하는 경우 Context Switching이 발생한다.  
>   
> 즉, **Context Switching은 프로세스가**   
> **Ready → Running,**  
> **Running → Ready,**  
> **Running → Block처럼**   
> **상태 변경 시에 발생**한다.

## Context Switching 수행 과정

1.  Task의 대부분 정보는 Register에 저장되고, PCB(Process Control Block)로 관리되고 있다.
2.  현재 실행하고 있는 Task의 PCB 정보를 저장하게 된다.(Process Stack, Ready Queue)
3.  다음 실행할 Task의 PCB 정보를 읽어 Register에 적재하고, CPU가 이전에 진행했던 과정을 연속적으로 수행할 수 있게 된다.

#### ※ Context Switching 시나리오

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FVQrAY%2FbtrXj09Vw8s%2FcuIwyIZvT5vwI49p2f7O0k%2Fimg.jpg)

> <시나리오 설명>  
> 1\. P0 프로세스가 인터럽트 되면서 PCB0에 P0 프로세스의 상태 정보를 저장한다.  
> 2\. 다음 수행할 P1 프로세스의 PCB1에서 P1 프로세스의 상태 정보가 CPU에 재로딩된다.  
> 3\. P1 프로세스를 일정 시간 수행한다.  
> 4\. P1 프로세스가 인터럽트 되면서, PCB1에 P1 프로세스의 상태 정보를 저장한다.  
> 5\. 다음 수행할 P0 프로세스의 PCB0에서 P0 프로세스의 상태 정보가 CPU에 재로딩된다.  
> 6\. P0 프로세스를 일정 시간 수행한다.  
>   
> ※ Context Switching과 Interrupt의 관계  
> CPU는 하나의 프로세스 정보만을 기억한다.  
> 여러 개의 프로세스가 실행되는 다중 프로그래밍 환경에서 CPU는  
> 각각의 프로세스의 정보를 저장했다 복귀하고 다시 저장했다 복귀하는 일을 반복한다.  
> 프로세스의 저장과 복귀는 프로세스의 중단과 실행을 의미한다.  
> 로세스의 중단과 실행 시 인터럽트가 발생하므로,  
> 문맥 교환이 많이 일어난다는 것은 인터럽트가 많이 발생한다는 것을 의미한다.

## Context Switching의 오버헤드

> 프로세스들의 시간 할당량은 시스템 성능의 중요한 역할을 한다.  
>   
> 시간 할당량이 적을수록 사용자 입장에서는  
> 여러 개의 프로세스가 거의 동시에 수행되는 느낌을 갖지만,   
> Context Switching의 수가 늘어난다.  
>   
> 프로세스의 실행을 위한 부가적인 활동을 **오버헤드**(간접 부담 비용)이라고 하는데,  
> 이 또한 Context Switching 수와 같이 늘어나게 된다.

정리하자면 다음과 같다.

-   시간 할당량이 적어지면 : Context Switching 수, 오버헤드가 증가하지만 여러 개의 프로세스가 동시에 수행되는 느낌을 갖는다.
-   시간 할당량이 커지면 : Context Switching 수, 오버헤드가 감소하지만 여러 개의 프로세스가 동시에 수행되는 느낌을 갖지 못한다.

전체적으로 봤을 때 이익이 되니까 overhead를 감수하더라도 Context Switching을 하는 것이고, 

그래서 운영체제가 CPU를 관리하는 것이다.

**사용자가 너무 기다리지 않게 관리**하기 위해서 반드시 해줘야 하는게 **Context Switching**이고,

이것이 대표적으로 운영체제가 하는 CPU관리 입니다.

---

## 예상 질문 겸 정리

> Q. 컨텍스트 스위칭이란 무엇인가?  
> A. **CPU가 어떤 하나의 프로세스를 실행하고 있는 상태**에서   
> 인터럽트 요청에 의해 다음 우선 순위의 프로세스가 실행되어야 할 때,   
> **기존의 프로세스의 상태 또는 레지스터 값(Context)을 PCB에 저장**하고,   
> **CPU가 다음 프로세스를 수행하도록 새로운 프로세스의 PCB 값을 불러와 교체**하는 작업이다.

---

### 출처

-   [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/PCB%20%26%20Context%20Switcing.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/PCB%20%26%20Context%20Switcing.md)
-   [https://m.blog.naver.com/adamdoha/222019884898](https://m.blog.naver.com/adamdoha/222019884898)
-   [https://junhyunny.github.io/information/operating-system/process-control-block-and-context-switching/](https://junhyunny.github.io/information/operating-system/process-control-block-and-context-switching/)