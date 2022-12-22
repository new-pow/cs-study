# 고유 락

## 멀티 스레드 환경에서의 동기화 문제

-   멀티 스레드 프로세서에서는 다른 스레드의 작업에 영향을 미칠 수 있다.
-   여러 스레드가 같은 자원을 공유하기 때문이다.
    -   자바 멀티 스레드 환경에서는 `static영역`과 `heap영역`을 공유한다.
    -   한 스레드가 작업하던 것을 다른 스레드가 넘어 갔을때 문제가 생긴다.
-   **진행 중인 작업이 다른 스레드에게 간섭받지 않게 하기 위해 ‘동기화’가 필요하다.**

```java
public class Counter {
	private int count;
	
	public int increase() {
		return ++count; // Thread-safe 하지 않은 연산
	}
}
// 1. read(count 값 읽기) -> 2. modify (count값 수정) -> 3. write (count값 저장) 과정에서 여러 Thread가 공유 자원 (count)으로 접근할 수 있으므로 동시성 문제 발생한다.
```

### ✨ 동기화란!
-   **스레드의 동기화 : 한 스레드가 진행중인 작업을 다른 스레드가 간섭하지 못하게 막는 것**
-   동기화를 하려면 간섭받지 않아야 하는 문장들을 ‘임계 영역’**으로 묶는다.
-   **임계영역은 락(lock)을 얻은 단 하나의 스레드만 출입 가능하다.**
    -   **객체 1개당 락 1개를 갖는다.**
    -   락이 없으면 객체의 임계영역에 들어갈 수 없다.

---

## 고유 락 Intrinstic lock

-   자바의 모든 객체는 락(lock)을 가지고 있다. == 고유 락
    -   `모니터`처럼 동작한다고 하여 monitor lock 혹은 monitor라고도 불린다.
-   **`synchronized`** 블록은 이 락을 다룬다.

```java
// synchronized 블록의 모양

synchronized(obj) {
	// critical section
}
```

### 예시 1
```java
// 기초 모양
public class Counter {
	// lock 생성
	private Object lock = new Object();
	
	private int count;
	
	public int increase() {
		synchronized(lock) {
			return ++count;
		}
	}
}
```

```java
// this를 이용하여 별도의 락 생성없이도 구현 가능하다.
public class Counter {
	private int count;
	
	public int increase() {
		synchronized(this) {
			return ++count;
		}
	}
}
```

```java
// 혹은 메서드 전체를 감싸는 경우에는 이렇게도 사용 가능하다.

public class Counter {
	private int count;
	
	public synchronized int increase() {
		return ++count;
	}
}
```

- `lock`이라는 `Object`의 instance를 사용하여 스레드가 동시에 `count` 변수에 접근하지 못하도록 제어한다. `increase()` 메서드는 한 번에 한 스레드만 실행할 수 있다.


### 예시 2
![](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ff4b6a960-066b-43b2-848e-5e2a4a5d561b%2FUntitled.png?id=8da01547-0573-4b3b-a53e-d025701319b1&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1680&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

```java
public class ThreadLockDemo {

    public static void main (String[] args) throws InterruptedException {
        ThreadLockDemo demo = new ThreadLockDemo();
        Thread thread1 = new Thread(() -> {
            System.out.println("thread1 before call "+ LocalDateTime.now());
            demo.syncMethod("from thread1");
            System.out.println("thread1 after call "+LocalDateTime.now());
        });
        Thread thread2 = new Thread(() -> {
            System.out.println("thread2 before call "+LocalDateTime.now());
            demo.syncMethod("from thread2");
            System.out.println("thread2 after call "+LocalDateTime.now());
        });

        thread1.start();
        thread2.start();
    }

    private synchronized void syncMethod (String msg) {
        System.out.println("in the sync method "+msg+" "+LocalDateTime.now());
        try {
            TimeUnit.SECONDS.sleep(5);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

```text
// output
thread1 before call 2016-03-27T18:08:30.872
thread2 before call 2016-03-27T18:08:30.872
in the sync method from thread1 2016-03-27T18:08:30.886
thread1 after call 2016-03-27T18:08:35.887
in the sync method from thread2 2016-03-27T18:08:35.887
thread2 after call 2016-03-27T18:08:40.887
```

---

## `synchronized`를 사용한 동기화의 특징

### 구조적인 락 structured lock
-   고유락을 이용한 동기화를 **구조적인락(structured lock)**이라고 한다.
-   `synchronized` 블록 단위로 락의 획득/해제가 일어나므로 구조적이라고 한다.
-   `synchronized` 블록을 진입할 때 락의 획득이 일어나고, 블록을 벗어날 때 락의 해제가 일어난다.
-   구조적인 락의 한계
    -   A와 B가 있을 때 `A lock 획득` -> `B lock 획득` -> `B lock 해제` -> `A lock 해제` 는 가능하다. (stack 처럼)
    -   `A lock 획득` -> `B lock 획득` -> `A lock 해제` -> `B lock 해제` 는 불가능하다.
    -   이렇게 사용하고 싶다면 `ReentrantLock` 과 같은 명시적인 락을 사용해야 한다.

### 재진입 가능성 Reentrancy
-   고유 락은 재진입이 가능하다.
-   락의 획득이 호출 단위가 아니라, 스레드 단위로 일어나기 때문이다.
-   이미 락을 획득한 스레드는 다시 같은 락을 얻기 위해 대기할 필요가 없다. 이미 락을 가지고 있으므로 같은 락에 대한 `synchronized` 블록을 만났을 때 대기없이 통과한다.

### ## 가시성 Visibility

-   이 코드는 두 스레드가 절대로 동시에 `increase()` 를 호출하는 일이 없다고 하더라도 문제가 있다.
-   한 스레드가 쓴 값을 다른 스레드가 볼 수도 있고 그렇지 않을 수도 있기 때문이다. 이를 가시성 문제라고 한다.
-   이 문제의 원인은 다양하다.
    -   최적화를 위해 컴파일러나 CPU에서 발생하는 코드 재배열(Reordering)때문에 이런 문제가 발생할 수도 있고,
    -   멀티 코어 환경에서는 코어의 캐시 값이 메모리에 제때 쓰이지 않아 문제가 발생할 수도 있다.
-   자바에서는 스레드가 락을 획득하는 경우 그 이전에 쓰였던 값들의 가시성을 보장한다.
-   `synchronized`가 적용된 `Counter` 예제에서 스레드 A, 스레드 B 순서로 `increase()`를 호출했을 때, 스레드 B는 스레드 A가 쓴 값을 읽을 수 있다(visible 하다).

---

## 스레드 안전한 객체란 무엇인가?

-   여러 스레드가 동시에 클래스를 사용하려 하는 상황에서 클래스 내부의 값을 안정적인 상태로 유지할 수 있다.
-   다양한 방법이 있다.
    -   블로킹 큐
    -   락
    -   자바 모니터 패턴
    -   조컨큐
    -   상태범위 제한
    -   위임기법
    -   동기화 컬렉션
    -   volatile
    -   인스턴스 한정
    -   스레드 한정
    -   threadlocal
    -   producer - consumer 패턴
- 이처럼 복잡한 상황이 많이 만들어진다.