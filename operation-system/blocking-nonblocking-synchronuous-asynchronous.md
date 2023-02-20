# 동기화-비동기화, 블로킹-논블로킹

> **동기와 블록킹**, **비동기와 논블록킹**의 작동 매커니즘이 더 직관적이기 때문에 많은 사람들이 이 개념들을 같은 것 혹은 비슷한 것으로 오해하고 있는데, 방금 이야기 했듯이 이 두가지 개념은 서로 전혀 다른 곳에 초점을 맞춘 개념들이므로 서로 직접적인 관련은 거의 없다고 봐도 된다. 단지 조합하여 사용되는 것 뿐이다. [출처](https://evan-moon.github.io/2019/09/19/sync-async-blocking-non-blocking/#%EB%8F%99%EA%B8%B0-%EB%B0%A9%EC%8B%9D--%EB%85%BC%EB%B8%94%EB%A1%9D%ED%82%B9-%EB%B0%A9%EC%8B%9D)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbfvMag%2FbtrZ7G8udRs%2F3onkMkDDXy80wbN1OlHlHk%2Fimg.png)

## **동기와 비동기 Synchronous, Asynchronous**

-   호출되는 함수의 작업 완료 여부를 누가 신경쓰는가에 따라 다르다.
-   동기/비동기는 **작업을 수행하는 주체**가 두 개 이상이어야 한다. 이 때 작업의 시간(시작, 종료 등)을 서로 맞춘다면 이를 동기라고 부르고, 서로 작업의 시간이 관계없다면 이를 비동기라고 부른다.

### **동기 Synchronous**

-   호출하는 함수가 호출되는 함수의 작업 완료 후 리턴을 기다리거나, 또는 호출되는 함수로부터 바로 리턴 받더라도 작업 완료 여부를 **호출하는 함수 스스로 계속 확인하며 신경쓰는 것.**

### **비동기 Asynchronous**

-   호출되는 함수에게 callback을 전달해서, 호출되는 함수의 작업이 완료되면 호출되는 함수가 전달받은 `callback`을 실행하고, **호출하는 함수는 작업 완료 여부를 신경쓰지 않는 것.**
-   시스템콜이 즉시 리턴될 때 데이터와 함께 오지 않는다.

---

## **블로킹과 논블로킹**

-   호출된 함수가 바로 리턴하느냐 마느냐
-   메서드를 사용하는 클라이언트의 입장에 대한 것이다.
-   블로킹/논블로킹은 **작업의 대상**이 2개 이상이어야 합니다. 

### **블로킹 Blocking**

-   A 함수가 B 함수를 호출 할 때, B 함수가 자신의 작업이 종료되기 전까지 A함수를 대기시키고 A 함수에게 제어권을 돌려주지 않는다.
-   대기 큐에 들어간다면
-   리턴은 시스템 콜이 완료된 후에 온다.

### **논블로킹 Non-Blocking**

-   A 함수가 B 함수를 호출 할 때, B 함수가 제어권을 바로 A 함수에게 넘겨주면서, A 함수가 다른 일을 할 수 있도록 한다.
-   대기 큐에 들어가지 않는다.
-   완료되지 않아도 빠르게 돌아온다.
-   시스템콜이 즉시 리턴될 때 데이터와 함께 온다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FvtzwN%2FbtrZYRXUF7j%2FRnLsCZVt6eVFEMvZ96EsS1%2Fimg.png)

---

## **ref.**

-   [Blocking-NonBlocking-Synchronous-Asynchronous](http://homoefficio.github.io/2017/02/19/Blocking-NonBlocking-Synchronous-Asynchronous/)
-   [Sync async-blocking-nonblocking-io](https://www.slideshare.net/unitimes/sync-asyncblockingnonblockingio)
-   [스프링캠프 2017 \[Day1 A2\] : Async & Spring](https://youtu.be/HKlUvCv9hvA)
-   [동기(Synchronous)는 정확히 무엇을 의미하는걸까?](https://evan-moon.github.io/2019/09/19/sync-async-blocking-non-blocking/#%EB%8F%99%EA%B8%B0-%EB%B0%A9%EC%8B%9D--%EB%85%BC%EB%B8%94%EB%A1%9D%ED%82%B9-%EB%B0%A9%EC%8B%9D)