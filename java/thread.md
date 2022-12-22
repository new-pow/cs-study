## Thread (스레드)란?

> 운영체제나 JVM에서 태스크(작업)을 실행하는 단위

→ 하나의 스레드는 하나의 작업밖에 수행할 수 없다.

<br><br><br>

#### ※ Java에서 스레드(Thread)란 무엇인가?

→ 스레드를 사용하기 전 기존 자바에서는 <br>
car.open();<br>
car.entrance();<br>
이렇게 코드 두 줄이 있다고 하면<br>
car.open()을 수행한 후에 car.entrance();를 수행하게 된다.<br><br>


즉, <br>
**위 코드를 수행 완료해야 아래 코드를 수행할 수 있다.**<br>
하지만 스레드를 사용하면<br>
car.open()을 수행하고 car.open()이 끝나지 않았음에도<br>
바로 car.entrance()를 수행하면서 아래 코드를 계속 수행하게 된다.<br>
그 말은<br>
**위 코드의 수행 완료여부와 상관없이 계속 코드들을 수행한다.** <br>
**(**스레드를 사용하면 한번에 여러 동작을 수행할 수 있다.)**** <br>

그렇다면 쓰레드를 사용하는 이유는 뭘까? <br>

쓰레드를 사용하면 동시에 여러개의 코드를 수행할 수 있으므로 <br>
쓰레드를 사용하여 많은 양도 한번에 처리할 수 있다. <br> <br>

🚨  **쓰레드를 사용 시 주의할 점이자 단점**

→ 쓰레드로 한번에 많은 코드들을 수행할수록 컴퓨터에 부하가 심해지며 <br>
쓰레드 수행 도중 내게 필요한 자원을 남이 가지고 있고 <br>
남은 남에게 필요한 자원을 내가 가지고 있어서 <br>
서로 무한정 대기하는 교착상태(Deadlock) 문제가 있으므로 이에 주의해야 함. <br> <br>

---
 <br>

## Multitasking (멀티태스킹)이란?
> 응용프로그램의 여러 작업(태스크)이 동시에 진행되게 하는 기법

**멀티태스킹의 2가지 방법**

1.  멀티프로세싱 (multi-processing)
2.  멀티스레딩 (multi-threading)

#### 1\. 멀티프로세싱

> 하나의 응용프로그램을 여러 개의 프로세스(process)로 구성하여  
> 각 프로세스가 하나의 작업(태스크)을 처리하도록 하는 기법

→ 자바에는 process가 존재하지 않고, 스레드 개념만 존재. JVM이 멀티스레딩만 지원

#### **2\. 멀티스레딩 (multi-threading)**

> 응용 프로그램을 여러개의 작업 단위로 나누고  
> 여러 개의 스레드가 각각 하나의 작업을 수행하도록 하는 방법 (자바는 멀티스레딩을 지원)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcgD8Bn%2FbtrUbxbuYI7%2Fknm3xglLpS0R5Uo3yhDSr0%2Fimg.jpg)

### 자바에서 멀티 스레딩

> 하나의 JVM은 하나의 자바 응용 프로그램만 실행  
> → 하나의 응용 프로그램은 하나 이상의 스레드로 구성 가능

자바에서 스레드 구현 방법은 2가지가 있다.

### 자바에서 스레드를 만드는 2가지 방법

> 자바는 멀티 스레드(Multi-Thread) 프로그래밍이 가능한 언어

방법 1. Thread 클래스를 상속한다.

방법 2. Runnable 인터페이스를 구현한다.

둘다 run() 메소드를 오버라이딩 하는 방식이다. (run()을 재정의)

start() 메소드를 호출해야 실행됨.

다음 예제는 

0부터 100까지의 숫자를 출력하는 **단일 스레드를 구성**하는 것이다.

#### **① Thread 클래스를 상속받는 방법**

```java
// 1. Thread 클래스를 상속한 후, 
// 2. Thread 클래스의 run() 메서드를 오버라이드 한다. (run() 메소드를 재정의)
// 3. main 메서드에서 객체를 생성한 후, 
// 4. start() 메서드를 호출해 주면 된다. (스레드 시작)

public class ThreadExtends extends Thread {

	@Override
	public void run() {
		int i=0;
		while(i <= 100){
			System.out.println("i==>" + i);
			i++;
		}
	}

	public static void main(String[] args){
		ThreadExtends th1 = new ThreadExtends();
		th1.start();
	}

}


// 출력결과
/*
i==>0
i==>1
i==>2
..........
i==>95
i==>96
i==>97
i==>98
i==>99
i==>100
*/
```

#### **② Runnable 인터페이스를 구현받는 방법**

Thread 클래스를 상속받아 구현하는 방법과 크게 다르지 않다.

run() 메서드를 강제로 오버라이드 해서 사용하면 되지만, 스레드의 객체를 생성하는 방법이 조금 다르다.

```java
// 1. Runnable 인터페이스로 새 클래스 구현
// 2. run() 메소드를 작성한다.
// 3. 스레드 객체 생성 (runnable target의 매개변수로 선언)
// 4. start()를 호출하여 스레드를 시작한다.

public class ThreadImplements implements Runnable {

	@Override
	public void run() {
		int i=0;
		while(i <= 100){
			System.out.println("i==>" + i);
			i++;
		}
	}
	
	public static void main(String[] args) {
         // Runnable Target으로 ThreadImplements의 객체를 넣어줌
		Thread th1 = new Thread(new ThreadImplements ()); 
		th1.start();
	}

}
```

여러 개의 스레드도 동시에 실행하여 멀티 스레드를 구현하는 것도 가능하다.

#### **멀티 스레드(Multi Thread) 구현하기**

> 여러 개의 스레드 객체를 생성하여 동시에 start() 메서드로 실행

0부터 100까지 1씩 증가하는 내용의 스레드 객체 3개를 생성하여 실행

단, 어떤 어떤 스레드가 실행되는지 구분이 어려우므로 id를 각각 1,2,3으로 설정하여 console에 찍어본다.

```java
public class MultiThread extends Thread {

	int id;

	public MultiThread(int id) {
		this.id = id;
	}

	@Override
	public void run() {
		int i=0;
		while(i < 100){
			System.out.println("id(" + this.id +"), i==>" + i);
			i++;
		}
	}

	public static void main(String[] args){
		MultiThread th1 = new MultiThread(1);
		MultiThread th2 = new MultiThread(2);
		MultiThread th3 = new MultiThread(3);
		
		th1.start();
		th2.start();
		th3.start();
	}
	
}


// 실행 결과 여러 개의 스레드가 동시에 실행되는 것을 확인할 수 있다.
/*
id(1), i==>0
id(2), i==>0
id(2), i==>1
id(2), i==>2
id(2), i==>3
id(2), i==>4
id(2), i==>5
id(2), i==>6
id(2), i==>7
id(2), i==>8
id(2), i==>9
id(2), i==>10
....
*/
```

### Thread 클래스 상속과 Runnable 인터페이스 구현의 차이

> 💡  자바는 다중 상속을 지원하지 않는다.  
> 그렇기 때문에 Thread 클래스를 상속받는 경우, 다른 클래스를 상속받을 수 없다.   
> 따라서 Runnable 인터페이스를 구현하는 것이 일반적이다.

### 스레드의 실행은 run() 호출이 아닌 start() 호출로 해야 한다.

> start()를 사용해야 멀티 쓰레드 프로그래밍 을 할 수 있다.

**start()** 메서드는 호출 시  새로운 쓰레드가 생성되고, 

생성된 쓰레드에서 run() 메서드가 실행된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcYcyBy%2FbtrUapSNB7F%2FEKlLfnR7MawE00Mc0UX2E0%2Fimg.png)

**run() 메서드를** 직접 호출하면 새로운 쓰레드가 생성되지 않고 현재 스레드에서 호출한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbs09JH%2FbtrUaqYwg8r%2FLiOmiTLhf79Ea218AY5kF1%2Fimg.png)

---

## 스레드 상태 5가지

1.  NEW : 스레드가 생성되고 아직 start()가 호출되지 않은 상태
2.  RUNNABLE : 실행 중 또는 실행 가능 상태
3.  BLOCKED : 스레드가 I/O 작업 요청을 하면 JVM이 자동으로 BLOCK 상태로 만듦 (lock이 풀릴 때까지 기다림)
4.  WAITING : 다른 스레드가 notify(), notifyAll()을 불러주기를 기다리고 있는 상태, **보통 스레드 동기화를 위해 사용**
5.  TIME\_WAITING : 스레드가 sleep(n)을 호출하여 n ms동안 잠을 자는 상태
6.  TERMINATED : 스레드 종료 상태

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F6an0x%2FbtrUaul7eUN%2Fe5EeArRCdjHQM9PAvEQBd0%2Fimg.png)

### 스레드 종료와 다른 스레드 강제 종료

-   스스로 종료하는 경우 : run() 메소드 리턴
-   다른 스레드에서 강제 종료하는 경우 : interrupt() 메소드 사용

```java
class TestThread extends Thread {
	int n=0;
    public void run() {
    	while(true) {
            n++;
            try {	
                Thread.sleep(1000);
            } catch (InterruptedException e) {
            	return;	// 예외 처리로 종료
            }
        }
    }
}
public class InterruptEx {
    public static void main(Stirng[] args) {
        TestThread thread = new TestThread();
        thread.start();
        thread.interrupt(); // 스레드 강제 종료
    }
}
```

### flag를 이용한 종료

-   스레드 안의 flag 변수를 이용하여 종료

```java
class TestThread extends Thread {
	int n=0;
    bool flag = false; // false로 초기화
    public void finish() {
    	flag = true;
    }
    public void run() {
    	while(true) {
            n++;
            try {
                Thread.sleep(1000);
                if (flag == true)
                	return;
            } catch (InterruptException e) {
            	return;
            }
        }
    }
}
public FlagEx {
	public static void main(String[] args) {
    	TestThread thread = new TestThread();
        thread.start();        
        tread.finish();	// TestThread 강제 종료
    }
}
```

---

## 스레드 동기화 (Thread Synchronization)

> 🚨  멀티스레드 프로그램 작성 시 주의점  
> → 다수의 스레드가 공유 데이터에 동시에 접근하는 경우  
> → 공유 데이터의 값에 예상치 못한 결과 발생 가능

💡 **이를 해결하기 위해 스레드 동기화 사용**

→ 진행 중인 작업이 다른 쓰레드에게 간섭받지 않게 하려면 '동기화'가 필요

→ 동기화를 통해 공유된 자원에 하나의 쓰레드만 접근 가능하게 할 수 있다.

동기화를 하려면?

→ 간섭받지 않아야 하는 문장들을 '**임계 영역**'으로 설정

→→ 임계 영역은 락(lock)을 얻은 단 하나의 쓰레드만 출입가능하다 (객체 1개에 락 1개)

### 1\. lock

> → 모든 객체에는 연결된 lock이 있다.   
> → 멀티 쓰레드가 공유된 자원에 접근할 때 lock을 사용  
> → 한 쓰레드가 lock을 사용하고 있으면 , 다른 쓰레드는 lock이 풀릴 때까지 기다린다.   
> → lock은 작업이 끝나면 풀린다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FclFrjJ%2FbtrUapk0jFV%2FBTk9XHmxW7zooe5MZx0DUK%2Fimg.png)

→ 쓰레드에서 synchronized 메소드가 호출되면 lock을 요청하여 얻어야 한다. 

→ 이때 다른 쓰레드에서 lock을 얻으려고 하면 blocked 된다.

-   synchronized 키워드로 임계영역을 설정 예제

```
//synchronized : 스레드의 동기화. 공유 자원에 lock
public synchronized void saveMoney(int save){    // 입금
    int m = money;
    try{
        Thread.sleep(2000);    // 지연시간 2초
    } catch (Exception e){

    }
    money = m + save;
    System.out.println("입금 처리");

}

public synchronized void minusMoney(int minus){    // 출금
    int m = money;
    try{
        Thread.sleep(3000);    // 지연시간 3초
    } catch (Exception e){

    }
    money = m - minus;
    System.out.println("출금 완료");
}
```

### 2\. wait()와 notify()

> 동기화의 효율을 높이기 위해 wait() , notify()를 사용

Object 클래스에 정의되어 있으며, 동기화 블록(임계 영역) 내에서만 사용할 수 있다.

-   wait() : 스레드가 lock을 가지고 있으면, lock 권한을 반납하고 대기하게 만듦
-   notify() : 대기 상태인 스레드에게 다시 lock 권한을 부여하고 수행하게 만듦

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FBFiuv%2FbtrT9OS7Hxp%2FXPWwKM7D8kQ2W2k0YqYUEk%2Fimg.png)

---

### 출처

-   [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Language/%5Bjava%5D%20Java%EC%97%90%EC%84%9C%EC%9D%98%20Thread.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Language/%5Bjava%5D%20Java%EC%97%90%EC%84%9C%EC%9D%98%20Thread.md "링크")
-   [https://velog.io/@jaejoengsin/java-%EB%A9%80%ED%8B%B0-%ED%83%9C%EC%8A%A4%ED%82%B9](https://velog.io/@jaejoengsin/java-%EB%A9%80%ED%8B%B0-%ED%83%9C%EC%8A%A4%ED%82%B9)
-   [https://velog.io/@ruthetum/JAVA-Thread-Multitasking](https://velog.io/@ruthetum/JAVA-Thread-Multitasking)
-   [https://deftkang.tistory.com/8](https://deftkang.tistory.com/8)
-   [https://m.blog.naver.com/varyeun/221694422391](https://m.blog.naver.com/varyeun/221694422391)
-   [https://tragramming.tistory.com/98](https://tragramming.tistory.com/98)
-   [https://connie.tistory.com/12](https://connie.tistory.com/12)[https://wakestand.tistory.com/93](https://wakestand.tistory.com/93)