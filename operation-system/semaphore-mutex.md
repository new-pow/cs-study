## ✔️ 들어가기 전...

뮤텍스와 세마포어를 알아보기 전, 임계구역(Critical Section)에 대해 먼저 정리하자.

## 💡 임계구역(Critical Section)이란?

> 여러 프로그램 혹은 쓰레드가 작업을 수행하면서 공유된 자원을 건드리게 될 수 있는데,  
> 이때 프로그램 코드 상에서 **공유 자원에 접근하는 부분**을 **임계구역**이라고 한다.

이렇게 임계 구역에 여러 프로세스 및 스레드가 함부로 접근할 수 없도록 

**데이터를 한 번에 하나의 프로세스만 접근할 수 있도록 제한을 두는 동기화 방식**을 취해야 한다.

동기화 도구에는 대표적으로 세마포어(Semaphore)와 뮤텍스(Mutex)가 있다.

🔒 이들은 모두 **공유된 자원의 데이터를 여러 스레드/프로세스가 접근하는 것을 막는 역할**을 한다.

세마포어는 일반화된 뮤텍스이다. 

따라서 뮤텍스에 대해 먼저 알아보자.

> 💡 뮤텍스와 세마포어의 차이는 서로 다른 방식으로 상호배제를 달성한다.   
> (※ 상호배제 : 오직 한 쓰레드만이 진입 가능함)

이제 이 둘을 알아보자.

---

## ✔️ 뮤텍스(Mutex) or 뮤텍스 락(Mutex Lock)

> 임계 구역을 가진 스레드들의 실행시간이 서로 겹치지 않고 각각 단독으로 실행되게 하는 기술이다.  
>   
> ※ 상호배제(**Mut**ual **Ex**clusion)의 약자임

해당 접근을 조율하기 위해 lock과 unlock을 사용한다.

-   lock : 현재 입계 구역에 들어갈 권한을 얻어온다.
    -   만약 다른 프로세스 / 스레드가 임계 구역 수행 중이면, 종료할 때까지 대기

-   unlock : 현재 임계 구역을 모두 사용했음을 알린다.
    -   대기 중인 다른 프로세스 / 스레드가 임계 구역에 진입할 수 있음

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbGAeYA%2FbtrXVhdt7wW%2FWAPsKJi9vfPzcMxAu4XXFK%2Fimg.png)

※ 영문 버전

더보기

![]()

## ✔️ 특징

-   세마포어와 마찬가지로, **병행 처리를 위한 동기화 기법** 중 하나이다.
-   동기화 대상이 **하나**이다.
-   임계구역을 가진 스레드들의 실행시간(Running Time)이 서로 겹치지 않고, 각각 단독으로 실행(상호배제)되도록 하는 기술이다.
-   프로세스나 스레드가 공유 자원을 lock()을 통해 잠금 설정하고, 사용한 후에는 unlock()을 통해 잠금 해제하는 객체이다.
-   잠금이 설정되면, 다른 프로세스나 스레드는 잠긴 코드 영역에 접근할 수 없고, 해제는 그와 반대이다.
-   또한 뮤텍스는 **잠금** 또는 **해제**라는 상태만을 가진다. (상태가 0, 1)
-   즉, 뮤텍스 객체를 두 스레드가 동시에 사용할 수 없다.

## 💡 예시를 들어보자.

뮤텍스는 **화장실이 '하나' 밖에 없는 식당**과 비슷하다.

화장실을 가기 위해서는 **카운터에서 열쇠를 받아가야** 한다.

당신이 화장실을 가려고 하는데 **카운터에 키가 있으면 화장실에 사람이 없다**는 뜻이고, 

당신은 그 열쇠를 이용해 화장실에 들어갈 수 있다고 가정하자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbq9C9x%2FbtrXVhq3GT9%2Fc7h1OJutJHb03cdskXwh8k%2Fimg.png)

> 카운터에 **열쇠가 없기 때문**에   
> **화장실에 사람(여자)가 있다는 뜻**이며, 남자는 화장실을 사용할 수 없다.  
> 즉, **여자가 나올 때까지 기다려야** 한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbjMgKv%2FbtrXVzdIAck%2FaRPBk5bbJc9ryBUSExKLLK%2Fimg.png)

> 곧이어 다른 남자도 화장실에 가고 싶어졌다.  
>   
> 이 남자 또한 화장실에 들어가기 위해서는 카운터에서 대기해야 한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcVrIT9%2FbtrXXgYMklx%2FbuKkuyQX3A5J3h3sASuavK%2Fimg.png)
> 이제 여자가 화장실에서 나와 카운터에 키를 돌려놓았다.  
>   
> 이제 기다리던 사람들 중 **맨 앞에 있던 사람**은 키를 받을 수 있고,   
> 이를 이용해 화장실을 갈 수 있다.

🙌🏻 이것이 뮤텍스가 동작하는 방식이다.

→ 화장실을 이용하는 사람이 **프로세스 혹은 쓰레드**이며, 

→ 화장실은 공유 자원, 

→ 화장실 키는 공유자원에 접근하기 위해 필요한 어떤 오브젝트이다.

## ✔️ 그래서 결국 뮤텍스가 뭔데?

> 💡 **뮤텍스는 오직 하나의 쓰레드만이 동일한 시점에 뮤텍스를 얻어 임계 영역에 들어올 수 있다.**  
>   
> 그리고 오직 이 쓰레드만이 임계 영역에서 나갈 때 뮤텍스를 해제할 수 있다.  
>   
> → 이러한 이유는, 뮤텍스가 1개의 락만을 갖는 매커니즘이기 때문이다.

※ 간단한 코드로 보자.

더보기

```
mutex = 1;

void lock () {
	while (mutex != 1) {
    	/* mutex 값이 1이 될 때까지 기다립니다.*/
    }
    /* 이 구역에 도착했다는 것은 mutex 값이 1이라는 것입니다.
       따라서 이제 뮤텍스 값을 0으로 만들어 다른 프로세스(혹은 쓰레드)가 접근하지 못하도록 막아야 합니다.
    */
    mutex = 0;
}

void unlock() {
	/* 임계 구역에서 나온 프로세스는 다른 프로세스가 접근할 수 있도록 락을 해제합니다.*/
	mutex = 1;
}
```

---

## ✔️ 세마포어(Semaphore)

> **멀티프로그래밍** 환경에서, 공유 자원에 대한 **접근을 제한**하는 방법이다.  
>   
> (여기서 말하는 '**접근을 제한**'하는 것이란?  
> → 공유된 자원의 데이터를 한 번에 하나의 프로세스만 접근할 수 있도록 하는 것)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbOyjJo%2FbtrXYrTBMcS%2FFds4AxK0U30pX8DXOHgvqK%2Fimg.png)

※ 영문 버전

더보기



## ✔️ 특징

-   세마포어는 일반화된 뮤텍스이다.
-   간단한 정수 값고 두 가지 함수 wait(P 함수라고도 함) 및 signal(V 함수라고도 함)로 공유 자원에 대한 접근을 처리한다.
-   wait()는 자신의 차례가 올 때까지 기다리는 함수이며, signal()은 다음 프로세스로 순서를 넘겨주는 함수이다.
-   프로세스나 스레드가 공유 자원에 접근하면, 세마포어에서 wait() 작업을 수행하고, 자원을 해제하면 세마포어에서 signal() 작업을 수항한다.
-   세마포어에는 조건 변수가 없고, 프로세스나 스레드가 세마포어 값을 수정할 때, 다른 프로세스나 스레드는 동시에 세마포어 값을 수정할 수 없다.

## 💡 예시를 들어보자.

세마포어는 손님이 화장실을 좀 더 쉽게 이용할 수 있는 레스토랑이다.

세마포어를 이용하는 레스토랑의 화장실에는 '**여러 개**'의 칸이 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcP7NKK%2FbtrXXx0UwUC%2FC6x8kZ2BPHQVpbNHSJebz0%2Fimg.png)

> 화장실 입구에는 **현재 화장실의 빈 칸 개수를 보여주는 전광판**이 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FCMYle%2FbtrXWgyDDtM%2FQBV06MYvAt56rGFV5Bf920%2Fimg.png)

> 만약 당신이 화장실에 가고 싶다면, 입구에서 빈 칸의 개수를 확인하고   
> **빈 칸이 1개 이상이라면 빈칸의 개수를 하나 뺀 다음에 화장실로 입장**해야 한다.  
>   
> 그리고 **나올 때 빈 칸의 개수를 하나 더해**준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbcUbcU%2FbtrXVxgnRgB%2F9HiPrxkQkyMOt8fJRXarU0%2Fimg.png)

> 만약 **모든 칸에 사람이 들어갔을 경우, 빈칸의 개수는 0**이 되며   
> 이때 화장실에 들어가고자 하는 사람이 있다면  
> **빈 칸의 개수가 1로 바뀔 때까지 기다려야** 한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcVTayo%2FbtrX0K6neGT%2FYKIgm5cVg3FFW4aiwUBbuk%2Fimg.png)

> 화장실을 나오면서 사람들은 빈 칸의 개수를 1씩 더한다.  
>   
> 그리고 기다리던 사람은 이 숫자에서 다시 1을 뺀 다음 화장실로 들어간다.

🙌🏻 이것이 세마포어가 동작하는 방식이다.

→ 세마포어는 공통으로 관리하는 하나의 값을 이용해(그림의 예제에서는 Num of Empty rooms) 상호배제를 달성한다.

→ 화장실이 공유 자원이며, 

→ 사람들이 쓰레드, 프로세스이다.

→ 화장실 빈 칸의 개수는 현재 공유자원에 접근할 수 있는 쓰레드, 프로세스의 개수를 나타낸다.

## ✔️ 세마포어의 종류

크게 **카운팅 세마포어(Counting Semaphores)**, **바이너리 세마포어(Binary Semaphore**) 2종류가 있다.

-   카운팅 세마포어
    -   세마포어의 카운트가 양의 정수값을 가진다.
    -   설정한 값만큼 쓰레드를 허용하고, 그 이상의 쓰레드가 자원에 접근하면 **락**이 실행된다.

-   바이너리 세마포어
    -   0과 1의 두 가지 값만 가질 수 있는 세마포어이다.
    -   Mutex처럼 사용될 수 있다. 🚨 하지만 뮤텍스는 절대로 세마포어처럼 사용될 수 없다.

※ 뮤텍스와 바이너리 세마포어의 차이

더보기

구현의 유사성으로 인해 뮤텍스는 바이너리 세마포어라고 할 수 있지만, 

엄밀히 말하면 뮤텍스는 **잠금**을 기반으로 상호 배제가 일어나는 '**잠금 매커니즘**'이고, 

세마포어는 **신호**를 기반으로 상호 배제가 일어나는 '**신호 매커니즘**'이다.

여기서 신호 매커니즘은 

휴대폰에서 노래를 듣다고 친구로부터 전호가 오면, 노래가 중지되고 통화 처리 작업에 관한 인터페이스가 등장하는 것을 상상하면 된다.

## ✔️ 그래서 결국 세마포어가 뭔데?

> 💡 **세마포어는 공유 자원에 세마포어의 변수만큼(여러 개)의 프로세스(또는 쓰레드)가 접근할 수 있다.**  
> (세마포어의 변수 → 공유자원의 개수를 나타내는 변수)  
>   
> 그리고 현재 수행 중인 프로세스가 아닌 다른 프로세스가 세마포어를 해제할 수 있다.

※ 간단한 코드로 보자.

더보기

```
struct semaphore {
	int count;
    	queueType queue;
};

void semWait (semaphore s) {
	s.count--;
    if (s.count < 0) 
    {
    	// 이 구역으로 들어왔다는 것은 현재 프로세스(스레드)가 공유 자원에 접근할 수 없다는 것을 의미.
    	// 요청한 프로세스를 s.queue에 연결 (대기 큐에 추가)
      // 요청한 프로세스를 블록 상태로 락
    }
} 

void semSignal (semaphore s) {
	s.count++;
    if (s.count <= 0) 
    {
    	// 대기하고 있는 프로세스(스레드)를 위해 s.queue에 연결되어 있는 프로세스를 큐에서 제거 (대키큐에서 기다리던 프로세스를 준비큐로 이동)
      // 프로세스의 상태를 실행 가능으로 변경하고 ready list에 연결
    }
}
```

---

## ✔️ 뮤텍스와 세마포어의 차이점

-   가장 큰 차이점은 **관리하는 동기화 대상의 갯수**이다.  
    -   Mutex는 동기화 대상이 **오직 1개**일 때 사용
    -   Semaphore는 동기화 대상이 **1개 이**상일 때 사용

-   세마포어는 뮤텍스가 될 수 있지만, 뮤텍스는 세마포어가 될 수 없다. (뮤텍스가 세마포어에 포함)
    -   Mutex는 0, 1로 이루어진 이진 상태이므로 Binary Semaphore라고 할 수 있음.

-   Mutex는 자원을 소유 + 책임을 가지는 반면, Semaphore는 자원 소유가 불가능하다. (아마 여러 개가 접근 가능해서 그럴까하는 건가... 이건 내 생각)
-   Mutex는 소유하고 있는 스레드 만이 이 Mutex를 해제할 수 있다. 반면, Semaphore는 Semaphore를 소유하지 않는 스레드가 Semaphore를 해제할 수 있다.
-   Semaphore는 시스템 범위에 걸쳐 있고 파일 시스템 상의 파일로 존재한다.  
    반면 Mutex는 프로세스의 범위를 가지며 프로세스 종료될 때 자동으로 Clean up된다.

뮤텍스와 세마포어는 모두 완벽한 기법은 아니므로 데이터의 무결성을 보장할 순 없으며

모든 교착상태를 해결하지는 못한다.

하지만 **상호배제를 위한 기본적인 문법**이기에 알아야 하는 지식이다.

---

## ✔️ 정리 겸 예상 질문

Q. 뮤텍스와 세마포어의 차이에 대해 설명해라.

A. 뮤텍스는 Lock을 사용해 하나의 프로세스나 쓰레드를 단독으로 실행하게 한다.

반면 세마포어는 공유자원에 세마포어 변수만큼의 프로세스(또는 쓰레드)가 접근할 수 있다.

또한 수행 중인 프로세스가 아닌 다른 프로세스가 세마포어를 해제할 수 있다.

하지만 뮤텍스는 락(lock)을 획득한 프로세스가 반드시 그락을 해제해야 한다.

아 어렵다 어려워;;;

---

### 출처

-   [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/Semaphore%20%26%20Mutex.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/Semaphore%20%26%20Mutex.md)
-   [https://github.com/JaeYeopHan/Interview\_Question\_for\_Beginner/tree/master/OS#%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%EB%8F%99%EA%B8%B0%ED%99%94](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/OS#%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%EB%8F%99%EA%B8%B0%ED%99%94)
-   [https://worthpreading.tistory.com/90](https://worthpreading.tistory.com/90)
-   [https://heeonii.tistory.com/14](https://heeonii.tistory.com/14)
-   [https://velog.io/@heetaeheo/%EB%AE%A4%ED%85%8D%EC%8A%A4Mutex%EC%99%80-%EC%84%B8%EB%A7%88%ED%8F%AC%EC%96%B4Semaphore%EC%9D%98-%EC%B0%A8%EC%9D%B4](https://velog.io/@heetaeheo/%EB%AE%A4%ED%85%8D%EC%8A%A4Mutex%EC%99%80-%EC%84%B8%EB%A7%88%ED%8F%AC%EC%96%B4Semaphore%EC%9D%98-%EC%B0%A8%EC%9D%B4)
-   [https://velog.io/@hidaehyunlee/Philosophers-%EC%98%88%EC%8B%9C%EC%98%88%EC%A0%9C%EB%A1%9C-%EB%B3%B4%EB%8A%94-%EB%AE%A4%ED%85%8D%EC%8A%A4%EC%99%80-%EC%84%B8%EB%A7%88%ED%8F%AC%EC%96%B4%EC%9D%98-%EC%B0%A8%EC%9D%B4](https://velog.io/@hidaehyunlee/Philosophers-%EC%98%88%EC%8B%9C%EC%98%88%EC%A0%9C%EB%A1%9C-%EB%B3%B4%EB%8A%94-%EB%AE%A4%ED%85%8D%EC%8A%A4%EC%99%80-%EC%84%B8%EB%A7%88%ED%8F%AC%EC%96%B4%EC%9D%98-%EC%B0%A8%EC%9D%B4)