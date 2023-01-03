# 💣 프로그램의 오류

프로그램은 세 가지로 나뉠 수 있다.

- **컴파일 에러** (compile-time error) 컴파일 할 때 발생하는 에러
- **런타임 에러** (runtime error) 실행할 때 발생하는 에러
- **논리적 에러** (logical error) 작성 의도와 다르게 동작

## 컴파일 에러

- 문법적 오류가 발생할 때 컴파일 에러가 발생한다.

```java
system.out.println("Hello world!");
```

- 컴파일 할 때 어떤 에러가 발생했는지 알려준다.
- class 파일이 만들어지지 않는다.

<aside>
👩🏻‍💻 참조 : 컴파일러가 하는 일
- 구문 체크
- 번역
- 최적화
- 생략된 코드 추가 : `extends Object` 등

</aside>


## 런타임 에러

- 실행 중 발생하는 에러
- 다양한 에러가 발생한다.
- IDE가 보조하여 알려준다.
- 실행하다 발생하면 프로그램이 종료된다.
- 런타임 에러의 종류 : 에러error와 예외exception
    - **error** : 프로그램 코드에 의해서 수습될 수 없는 심각한 오류. 개발자가 미리 예측하여 방지할 수 없다. (OutOfMemory error 등)
    - **exception** : 프로그램 코드에 의해서 수습될 수 없는 다소 미약한 오류. 개발자가 구현한 로직에서 발생한 실수나 사용자의 영향에 의해 발생. 개발자가 미리 예측하여 방지할 수 있다.
- 에러는 어쩔 수 없지만, 예외는 처리하자.

## 논리적 에러

- 프로그램은 잘 시행이 되나, 의도와 다르게 동작할 때

---

# 🛠️ Error & Exception 클래스 구조

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F4dd0c5f6-41f3-4dc2-b220-a25d55b38d6b%2FUntitled.png?id=0f6a4671-60c5-48a5-a3a6-e51b90358500&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1680&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

- Throwable : 클래스, 모든 오류의 조상
- Exception : 런타임에러 중 미약한 오류
- Error : 런타임에러 중 심각한 오류

## Throwable??

- 오류와 예외 모두 자바 최상위 클래스 Object의 상속을 받는다.
- 그 사이 `Throwable` 클래스가 있는데, 오류나 예외에 대한 메시지를 담는 메서드와 예외가 연결될 때(chained exception) 연결된 예외 정보들을 기록하고 출력하는 메서드를 가진다.
    - `getMessage()`
    - `printStackTrace()`

## Checked Exception - Unchecked Exception

### 체크 예외 Checked Exception

- RuntimeException 클래스 외 Exception의 자손들
- 반드시 에러 처리를 해야한다. (try/catch or throw)
- 사용자의 실수와 같은 외적인 요인에 의해 발생하는 예외
    - 입출력 예외
    - 파일을 찾지 못하는 경우
    - 이름이 잘못되어 클래스 찾지 못하는 경우 등


### 언체크 예외 Unchecked Exception

- RuntimeException과 그 자손들
- 반드시 에러 처리를 강제하지 않는다.
- 실행중에 발생할 수 있는 예외를 의미한다.
- 프로그래머의 실수로 발생하는 예외
    - 산술 계산할 때 예외 (5/0)
    - 형변환 예외
    - nullPoint 예외
    - IndexOutOfBounds 예외(배열 범위 벗어남)

|  | 체크 예외 | 언체크 예외 |
| --- | --- | --- |
| 예외처리 여부 | 반드시 예외 처리해야함 | 명시적인 처리를 강제하지 않음 |
| 확인 시점 | 컴파일 단계 | 실행단계 |
- [참고영상 : ****자바 공부를 어떻게 하길래, "언체크드 예외 발생시 트랜잭션 롤백?"****](https://youtu.be/_WkMhytqoCc)

## 예외 클래스의 계층 구조

- 전체 종류 [Exception과 Error 종류와 발생 원인](https://www.notion.so/Exception-Error-0dde35de4d54490ca0ba7aba7090cadf)

![[https://www.atatus.com/blog/types-of-exceptions-in-java/](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F8d552bba-31bb-411c-b3b0-652b360a3bd8%2FUntitled.png?id=f62d37fc-b5b0-4ad0-9f77-aad3cc26ac26&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1680&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

[https://www.atatus.com/blog/types-of-exceptions-in-java/](https://www.atatus.com/blog/types-of-exceptions-in-java/)

| Basis of Comparison | Exception | Error |
| --- | --- | --- |
| Recoverable/ Irrecoverable | try-catch 블록으로 처리할 수 있다. | 커버가 불가능 |
| Type | checked 와 unchecked로 나뉜다. | 모두 unchecked error |
| Occurrence | compile time이나 run time에서 발생한다. | run time에서 발생한다. |
| Package | java.lang.Exception package | java.lang.Error package |
| Known or unknown | 체크 예외만 compiler에 알려짐. | Errors will not be known to the compiler. |
| Causes | 대부분 application 에 의해 발생 | 대부분 application 의 환경에 의해 발생 |
| Example | Checked Exceptions:SQLException, IOExceptionUnchecked Exceptions:ArrayIndexOutOfBoundException, NullPointerException, ArithmaticException | Java.lang.StackOverFlow, java.lang.OutOfMemoryError |

[https://www.javatpoint.com/exception-vs-error-in-java](https://www.javatpoint.com/exception-vs-error-in-java)

# 🛠️ 예외 처리 exception handling

- 정의 : 프로그램 실행시 발생할 수 잇는 예외 발생에 대비한 코드를 작성하는 것
- 목적 : **프로그램의 비정상 종료**를 막고, 정상적인 실행상태를 유지하는 것

## 예외가 주로 발생하는 원인

- 사용자의 잘못된 데이터 입력
- 잘못된 연산
- 개발자가 로직을 잘못 작성
- 하드웨어, 네트워크 오작동
- 시스템 과부하

## 예외 처리 try-catch

```java
try {
	// 예외 발생할 가능성이 있는 문장들
} catch (Exception1 e1) {
	// exception1 에 대한 처리 코드
} catch (Exception2 e2) {
	// exception2 에 대한 처리 코드
} catch (Exception3 e3) {
	// exception3 에 대한 처리 코드
}
```

- 주의!! if문과는 달리 `{}`를 생략할 수 없다.
- try 블럭 내에서 예외가 발생했다면?
    1. 일치하는 예외 `catch` 블럭이 있는 지 확인
    2. 있다면, `catch` 블럭 내의 코드를 수행하고, `try-catch`를 빠져나가 다음 문장부터 수행한다.
    3. 없다면, 예외는 처리되지 못한다.
- try 블럭 내에서 예외가 발생하지 않았다면?
    1. `catch` 블럭을 거치지 않고 전체 `try-catch` 를 빠져나가 다음 문장부터 수행한다.
    2. 만약 여러개 `catch` 가 있을 경우, 해당하는 예외의 최초 `catch`블록을 수행하고 빠져나온다.


## 예외 객체

### 예외가 발생하면 어떤 일이 일어날까?

```java
try {
	int i = 0/0;
} catch (ArithmeticException ae) {
	ae.printStackTrace();
	System.out.println(ae.getMessage());
} catch (Exception e) {
	// exception3 에 대한 처리 코드
}
```

- 메모리에 예외 객체 생성된다.
    - 위의 예시에서는 `ArithmeticException` 타입인 객체 생성
    - 참조 변수 `ae` 에 객체 주소가 저장된다.
- 객체 안에는 예외 정보가 들어있다.
- 예외 클래스 메서드를 갖고 있다. `printStackTrace()`, `getMessage()` 등...


### 예외 객체의 메서드

- `printStackTrace()`
    - 예외 발생 당시의 호출 스택(Call Stack)에 있었던 메서드의 정보와 예외 메시지를 화면에 출력한다. 반환값은 void.
- `getMessage()`
    - 발생한 예외클래스의 인스턴스에 저장된 메시지 String 타입을 얻을 수 있다.
- `getStackTrace()`
    - jdk1.4 부터 지원, printStackTrace()를 보완, StackTraceElement[] 이라는 문자열 배열로 변경해서 출력하고 저장한다.

## finally

- 프로그램 시행 중 어떤 예외가 발생하더라도 반드시 실행되어야 하는 부분이 있다면 어떻게 할까?

```java
try {
	int i = 0/0;
} catch (ArithmeticException ae) {
	ae.printStackTrace();
	System.out.println(ae.getMessage());
} catch (Exception e) {
	// exception3 에 대한 처리 코드
} finally {
	// 예외에 상관없이 무조건 수행되는 코드
}
```

---

# 🔥 예외 발생시키기

- 적극적으로 예외를 발생시킬 수 있다.

### 방법1. `RuntimeException` 을 상속받아 예외를 구현한다.

- `RuntimeException` : 프로그램 실행시 발생하는 예외

```java
class FoolException extends RuntimeException {
}

public class Sample {
    public void sayNick(String nick) {
        if("fool".equals(nick)) {
            throw new FoolException();
        }
        System.out.println("당신의 별명은 "+nick+" 입니다.");
    }

    public static void main(String[] args) {
        Sample sample = new Sample();
        sample.sayNick("fool");
        sample.sayNick("genious");
    }
}
```

### 방법2. `Exception` 을 상속받아 구현한다.

- `Exception` 은 컴파일 시 발생하는 예외이다.
- 위와 같은 예시에는 컴파일 오류가 발생한다.
    - 아래처럼 try-catch 구문으로 처리하면 컴파일 오류를 막을 수 있다.
- `sayNick` 메서드에서 `FoolException`을 발생시키고 예외처리도 `sayNick` 메서드에서 했다.

```java
class FoolException extends Exception {
}

public class Sample {
    public void sayNick(String nick) {
        try {
            if("fool".equals(nick)) {
                throw new FoolException();
            }
            System.out.println("당신의 별명은 "+nick+" 입니다.");
        }catch(FoolException e) {
            System.err.println("FoolException이 발생했습니다.");
        }
    }

    public static void main(String[] args) {
        Sample sample = new Sample();
        sample.sayNick("fool");
        sample.sayNick("genious");
    }
}
```

---

# ⚾️ 예외 던지기 throws

- 예외 처리 회피라고도 한다.
- `sayNick` 을 호출한 곳에서 `FoolException` 을 처리하도록 예외를 위로 던질 수 있는 방법
- throws 라는 구문을 메서드 뒷부분에 삽입하여 호출한 곳으로 위로 보낼 수 있다.
- “예외를 뒤로 미룬다” 라고도 한다.
- 이제 예외를 처리해야 하는 대상이 sayNick 메서드에서 main 메서드로 변경되었다.

```java
public class Sample {
    public void sayNick(String nick) throws FoolException {
        try {   // try .. catch 문을 삭제할수 있다.
            if("fool".equals(nick)) {
                throw new FoolException();
            }
            System.out.println("당신의 별명은 "+nick+" 입니다.");
        }catch(FoolException e) {
            System.err.println("FoolException이 발생했습니다.");
        }
    }

    public static void main(String[] args) {
        Sample sample = new Sample();
        sample.sayNick("fool");
        sample.sayNick("genious");
    }
}
```

- 다음과 같이 변경한다.

```java
class FoolException extends Exception {
}

public class Sample {
    public void sayNick(String nick) throws FoolException {
        if("fool".equals(nick)) {
            throw new FoolException();
        }
        System.out.println("당신의 별명은 "+nick+" 입니다.");
    }

    public static void main(String[] args) {
        Sample sample = new Sample();
        try {
            sample.sayNick("fool");
            sample.sayNick("genious");
        } catch (FoolException e) {
            System.err.println("FoolException이 발생했습니다.");
        }
    }
}
```

## 🤔 예외 처리, 어디서 하는게 좋을까?

- 위의 예시와 같이 호출된 메서드에서 직접 예외 처리를 할 수도 있고, 아니면 호출한 곳으로 던져 main에서 예외처리를 할 수도 있다. 과연 어디서 하는 것이 좋을까?
- 두 방법의 차이점에는 ‘어디까지 코드를 실행할 것인가’라는 문제가 걸려있다.
1. 메서드 내에서 예외처리할 경우

```java
public class Sample {
    public void sayNick(String nick)  {
        try {
            if("fool".equals(nick)) {
                throw new FoolException();
            }
            System.out.println("당신의 별명은 "+nick+" 입니다.");
        }catch(FoolException e) {
            System.err.println("FoolException이 발생했습니다.");
        }
    }

    public static void main(String[] args) {
        Sample sample = new Sample();
        sample.sayNick("fool");
        sample.sayNick("genious"); // 여기까지 시행한다.
    }
}
```

```
// output
FoolException이 발생했습니다.
FoolException이 발생했습니다.
```

1. Main 에서 예외처리를 할 경우

```java
class FoolException extends Exception {
}

public class Sample {
    public void sayNick(String nick) throws FoolException {
        if("fool".equals(nick)) {
            throw new FoolException();
        }
        System.out.println("당신의 별명은 "+nick+" 입니다.");
    }

    public static void main(String[] args) {
        Sample sample = new Sample();
        try {
            sample.sayNick("fool"); // 이것을 시행하다가 catch로 빠진다.
            sample.sayNick("genious");
        } catch (FoolException e) {
            System.err.println("FoolException이 발생했습니다.");
        }
    }
}
```

```
// output
FoolException이 발생했습니다.
```

- 이러한 이유로 예외 처리 위치가 매우 중요하다.
- 프로그램의 수행 여부를 결정하고, 트랜잭션과도 밀접한 관계가 있다.
    - 참고 : [트랜잭션 Transaction](https://www.notion.so/Transaction-fffe0b721c97453990841c069af58a06)

---

# 연결된 예외 chained exception

- 특정 예외에서 다른 예외를 발생시키는 것
- A예외에서 B예외 처리 블록으로 유도할 수 있다.
- 예외 전환이라고도 한다.

## 연결된 예외를 왜 사용하나?

- 체크 예외를 RuntimeException으로 감싸 언체크 예외로 바꿀 수 있다.
- 이 기능을 사용해 더이상 억지로 try-catch로 처리해줄 필요가 없어진다.
    - 아래 예시에서 `MemoryException` 는 무조건 `try-catch` 해줘야 하는데, 이는 사실상 코드로 처리할 수 없어 의미없는 `catch` 가 된다.
    - 이를 `RuntimeException` 으로 wrapping 하여 불필요한 `catch` 블럭을 삭제할 수 있다.

```java
try{
    startInstall();
    copyFiles();
}catch(SpaceException ex){
    InstallException ie = new InstallException("설치중 예외 발생");
    ie.initCause(ex);
    throw new RuntimeException(ie);
}
/*catch (MemoryException me){
    //....
}*/
```

### 방법

1. 연결할 새로운 예외 객체 생성한다.
2. 새로운 예외객체에 `initCause` 메서드에 인자값으로 기존 연결될 예외 객체를 넣어준다.
    1. `initCause` 는 `Trowable` 에 정의되어 있는 메서드이다.
3. `throw` 로 연결할 예외 객체를 던진다.

---

# 😉 예외 처리 방법

- 일반적인 예외 처리의 방법 3가지
![](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F1f2395f2-95ac-48bd-822e-bd49e37be284%2FUntitled.jpeg?id=537cf858-0076-4195-b009-5b0a2077156c&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1680&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)
- 예외 복구 : 다른 작업 흐름으로 유도
- 예외처리 회피 : 호출한 쪽으로 던지기
- 예외 전환 : 호출한 쪽으로 던질 때 명확한 의미 전달을 위해 다른 예외로 전환하여 던지기

## 1. 예외 복구

```java
int maxretry = MAX_RETRY;
while(maxretry -- > 0) {
    try {
        // 예외가 발생할 가능성이 있는 시도
        return; // 작업성공시 리턴
    }
    catch (SomeException e) {
        // 로그 출력. 정해진 시간만큼 대기
    } 
    finally {
        // 리소스 반납 및 정리 작업
    }
}
throw new RetryFailedException(); // 최대 재시도 횟수를 넘기면 직접 예외 발생
```

- 예외가 발생하여도 애플리케이션은 정상적인 흐름으로 진행된다.
- 예시의 경우, 예외가 발생하면 그 예외를 일정 시간만큼대기하고 다시 재시도를 반복하다 최대 재시도 횟수를 넘기면 예외를 발생시킨다.
- 재시도를 통해 정상적인 흐름을 타게 한다거나, 예외 발생을 미리 예측하여 다른 흐름으로 유도시키도록 구현하면 비록 예외가 발생하였어도 정상적으로 작업을 종료할 수 있다.

## 2. 예외처리 회피 : 예외 던지기 참조

- 호출한 쪽에서 다시 예외를 받아 처리하도록 하거나, 해당 메소드에서 이 예외를 던지는 것이 최선의 방법이라는 확신이 있을 때만 사용한다.

## 3. 예외 전환 : 연결된 예외 참조

- 호출한 쪽에서 예외를 받아서 처리할 때 좀 더 명확하게 인지할 수 있도록 돕기 위한 방법
- 어떤 예외인지 분명해야 처리가 수월해지기 때문이다.

---

- 참고
    - 자바의 정석 chapter 8
    - [https://movefast.tistory.com/12?category=765934](https://movefast.tistory.com/12?category=765934)
    - [https://mangkyu.tistory.com/152](https://mangkyu.tistory.com/152)
    - [https://www.nextree.co.kr/p3239/](https://www.nextree.co.kr/p3239/)