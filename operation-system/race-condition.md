## ✔️ 동기 (Synchronous)와 비동기(Asynchronous)

> 데이터 처리 방식

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbT7QTt%2FbtrXPssGILZ%2FA9kFBcY2TeAQlNtHsdB9S1%2Fimg.jpg)

## 💡 동기 (Synchronous)

> 서버에서 요청을 보냈을 때, **응답이 돌아와야 다음 동작을 수행**할 수 있다.  
>   
> 즉, A 작업이 모두 진행될 때까지 B 작업은 대기해야 한다.

-   간단하고 직관적임
-   어떠한 일을 처리하는 동안, 다른 일을 하지 못함
-   작업 완료 여부를 호출한 쪽에서 신경을 씀

## 💡 비동기 (Asynchronous)

> 동기와 반대로, 요청을 보냈을 때 **응답 상태와 상관 없이 다음 동작을 수행**할 수 있다.  
>   
> 즉, A 작업이 시작하면 동시에 B 작업도 실행된다. A 작업은 결과값이 나오는대로 출력된다.

-   동기보다 복잡함
-   어떠한 일을 처리하는 동안 다른 일을 할 수 있어 자원을 효율적으로 사용 가능함
-   작업 완료 여부를 호출된 쪽에서 신경을 씀

### ※  Blocking I/O & Non-Blocking I/O

더보기

💡 Blocking I/O : 호출된 함수가 **자신의 작업을 모두 끝낼 때까지 제어권을 가지고 있어**, 호출한 함수가 대기하도록 한다.

💡 Non-Blocking I/O : 호출된 함수가 바로 return해서 **호출한 함수에게 제어권을 주어 다른 일을 할 수 있게** 한다.

---

**Blocking I/O & Synchronous와** **Non-Blocking I/O & Asynchronous는 서로 비슷한 개념이므로 생략** 

💡 Non-Blocking I/O  & Synchronous : Non-Blocking은 바로 리턴을 해서 **제어권을 넘겨**주고, 

Sync는 작업완료 여부를 호출한 쪽에서 신경을 쓴다.

즉, 호출을 하고 반환이 되고, 다른 일을 수행하는데 작업이 완료되었는지 계속 물어보는 일을 추가로 수행한다.

💡 Blocking I/O  & Asynchronous : Blocking 방식은 작업이 끝날 때까지 **제어권을 계속 가지**고, 

Async는 작업완료 여부를 호출된 쪽에서 신경을 쓴다.

이 방식은 특별한 장점이 없어 일부러 사용되진 않는다.

---

## ✔️ 프로세스 동기화

> 프로세스 동기화란, 하나의 자원을 하나의 프로세스만이 이용하도록 제어하는 것이다.

## ❓ 왜 필요할까?

> 프로세스들이 독립적이지 않고, 서로 협조하여 **공통된 자원을 서로 접근하**기 때문에 프로세스끼리 영향을 미친다.  
> 프로세스가 1개가 아니라 멀티라 발생하는 문제였고, 이것을 해결하기 위해 **프로세스 동기화가 필요**하다.

---

## ✔️ 경쟁 상태  (Race Condition)

> Race Condition(경쟁상태)이란,   
> 여러 개의 프로세스가 **공유 자원에 동시 접근**할 때, **실행 순서에** 따라 **결과값이 달라질 수 있는 현상**이다.  
> → 이 한 문장이 race conditon(경쟁 상태)에 대한 모든 것이다.  
>   
> 즉, 공유 자원을 두 개 이상의 프로세스가 동시에 읽거나 쓰는 상황을 뜻한다.  
> (결과값에 영향을 주는 상태)

비동기 맥락에서 race conditon은 주로 **요청 순서와 응답 순서가 반드시 같지는 않음**을 의미하는 용어로 사용된다.

🚨 경쟁 상태는 컴퓨터 입장에서 아주 큰 문제다.

왜냐?

똑같은 코드를 100번 돌리면 실행 결과가 항상 같아야 하는데, 경쟁 상태가 발생하면 결과가 달라질 수 있기 때문이다.

예시를 들어보자.

종선코인 100개가 있다고 가정해보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbaEZMb%2FbtrXVkGB4nl%2FhRpEJRTrxFwrFgh11XRNq1%2Fimg.png)

→ 프로세스 A와 프로세스 B가 동시에 접근하여, 타이밍이 서로 꼬였다.

정상 결괏값은 300인데, 200이 출력된다.

💡 이러한 문제를 방지하기 위해, 공유 메모리를 쓰는 **프로세스끼리 '동기화'를 해줘야** 한다.

∴ 정리하면,

> **공유 메모리를 쓰는 프로세스끼리는 경쟁상태가 발생할 수 있는데, 이에 대한 해결책이 동기화다.**

## ✔️ 경쟁 상태(Race Condition)가 발생하는 경우

1\. 커널 작업을 수행하는 중에 **인터럽트**가 발생

-   문제점 : 커널모드에서 데이터를 로드하여 작업을 수행하다가 인터럽트가 발생하여 같은 데이터를 조작하는 경우
-   해결법 : 커널모드에서 작업을 수행하는 동안, 인터럽트를 disable 시켜 CPU 제어권을 가져가지 못하도록 한다.

2\. 프로세스가 'System Call'을 하여 커널모드로 진입하여 작업을 수행하는 도중 **문맥 교환**이 발생할 때

-   문제점 : 프로세스 1이 커널모드에서 데이터를 조작하는 도중, 시간이 초과되어 CPU 제어권이 프로세스 2로 넘어가, 같은 데이터를 조작하는 경우 (프로세스 2가 작업에 반영되지 않음)
-   해결법 : 프로세스가 커널모드에서 작업을 하는 경우 시간이 초과되어도 CPU 제어권이 다른 프로세스에게 넘어가지 않도록 한다.

3\. 멀티 프로세서 환경에서 공유 메모리 내의 커널 데이터에 접근할 때

-   문제점 : 멀티 프로세서 환경에서 2개의 CPU가 **동시에 커널 내부의 공유 데이터에 접근**하여 조작하는 경우
-   해결법 : 커널 내부에 있는 각 공유 데이터에 접근할 때마다, 그 데이터에 대한 lock/unlock을 하는 방법

## ✔️ 경쟁 상태의 해결 방안 - 동기화

> 경쟁상태는 **메모리를 공유하기 때문**에 발생한다❗❗  
> 그럼 해결 방안은?  
> **동기화**❗❗

경쟁상태가 발생하지 않게 하는 방법이 있다.

바로 **'쓰레드의 순차적 실행'을 보장**해주면 된다.

→ 이것을 **'동기화'**라고 부른다.

---

## ✔️ 프로세스 동기화의 임계 영역 (Critical Section)

> 둘 이상의 프로세스, **스레드가 공유 자원(Ex. 공유하는 변수 사용, 동일 파일을 사용하는 등)에 접근**할 때,  
> 순서 등의 이유로 **결과가 달라지는 영역**을 말한다.  
>   
> 즉, 여러 개의 쓰레드가 수행되는 시스템에서 각 쓰레드들이 **공유하는 데이터를 변경하는 코드 영역**을 말한다.  
> 이는 동기화에서 중요한 문제 중 하나이다.

💡 임계 영역(구역)을 해결하기 위해서는 다음 3가지 조건을 만족해야 한다.

1.  Mutual exclusion(상호배타 or 상호배제) : 오직 한 쓰레드만이 진입 가능하다. 한 쓰레드가 입계영역에서 수행 중인 상태에서는 다른 쓰레드는 절대 이 구역에 접근할 수 없다.
2.  Progress(진행 or 융통성) : 임계 영역에 들어간 프로세스가 있지 않은 상태에서 임계 영역에 들어가려는 프로세스가 있으면 들어가게 해주어야 한다. 즉, 임계영역에 있는 프로세스 외에는 다른 프로세스가 임계 영역에 진입하는 것을 방해하면 안된다.
3.  Bounded waiting(유한 대기 or 한정대기) : 임계영역으로 진입하기 위해 대기하는 모든 쓰레드는 유한 시간 이내에 해당 임계영역으로 진입할 수 있어야 한다.

※ 한줄 정리

더보기

\- 상호 배제 : 한 프로세스가 임계 영역에 들어갔을 때, 다른 프로세스는 들어갈 수 없다.

\- 융통성 : 한 프로세스가 다른 프로세스의 일을 방해해서는 안 된다.

\- 한정 대기 : 특정 프로세스가 영원히 임계 영역에 들어가지 못하면 안 된다.

위의 세 조건을 만족하는 방법은 크게 **뮤텍스**, **세마포어**, **모니터**가 있다.

뮤텍스와, 세마포어에 대해서는 다음 포스팅에 담을 예정이다.

🔒 이 방법에 토대가 되는 메커니즘은 **잠금(lock)**이다.

예를 들어, 임계 영역을 화장실이라 해보자.

화장실에 A라는 사람이 들어간 다음 문을 잠근다. 

그리고 다음 사람이 이를 기다리다가 A가 나오면 화장실을 쓰는 것이다.

## ✔️ 결국 프로세스 / 쓰레드 동기화 목적이 뭔데?

-   **임계구역 문제 해결** (틀린 답이 나오지 않도록)
-   **프로세스 실행 순서 제어** (원하는대로)

## ✔️ 프로세스 동기화 방법

[뮤텍스, 세마포어, 모니터 등 다음 포스팅에서 다룸.](https://ummmmchicken.tistory.com/entry/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%EC%84%B8%EB%A7%88%ED%8F%AC%EC%96%B4Semaphore-%EB%AE%A4%ED%85%8D%EC%8A%A4Mutex-%EB%AA%A8%EB%8B%88%ED%84%B0-Monitor)

---

## ✔️ 정리 겸 예상 질문

Q. 임계영역이란 무엇인가?

A. 임계영역은 공통 데이터를 변경하는 구간을 말한다.

Q. 임계구역의 문제를 해결할 수 있는 조건은?

A. 문제를 해결하기 위해서는 상호배타, 진행, 유한대기를 만족시켜야 한다.

**상호배타**는 임계영역에 하나의 스레드만 진입하는 것이고, 

**진행**은 누가 먼저 들어갈지에 대해 유한시간 내에 이루어져야 하는 것이고, 

**유한대기**는 어느 스레드라도 유한 시간 내에 임계 영역에 접근이 가능한 것이다.

---

### 출처

-   [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/Race%20Condition.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/Race%20Condition.md)
-   [https://charles098.tistory.com/88](https://charles098.tistory.com/88)
-   [https://zangzangs.tistory.com/115](https://zangzangs.tistory.com/115)
-   [https://tecoble.techcourse.co.kr/post/2021-09-12-race-condition-handling/](https://tecoble.techcourse.co.kr/post/2021-09-12-race-condition-handling/)
-   [https://iredays.tistory.com/125](https://iredays.tistory.com/125)
-   [https://github.com/JaeYeopHan/Interview\_Question\_for\_Beginner/tree/master/OS#%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%EB%8F%99%EA%B8%B0%ED%99%94](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/OS#%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%EB%8F%99%EA%B8%B0%ED%99%94)
-   [https://velog.io/@daybreak/%EB%8F%99%EA%B8%B0-%EB%B9%84%EB%8F%99%EA%B8%B0-%EC%B2%98%EB%A6%AC](https://velog.io/@daybreak/%EB%8F%99%EA%B8%B0-%EB%B9%84%EB%8F%99%EA%B8%B0-%EC%B2%98%EB%A6%AC)
-   [https://lu-coding.tistory.com/15](https://lu-coding.tistory.com/15)