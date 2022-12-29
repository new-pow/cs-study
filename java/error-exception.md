# 💣 프로그램의 오류

세 가지로 나뉠 수 있다.

1. **컴파일 에러** (compile-time error) 컴파일 할 때 발생하는 에러
2. **런타임 에러** (runtime error) 실행할 때 발생하는 에러. `Error` 와 `Exception` 으로 나뉜다.
3. **논리적 에러** (logical error) 작성 의도와 다르게 동작

## 1. 컴파일 에러

-   문법적 오류가 발생할 때 컴파일 에러가 발생한다.

```java
system.out.println("Hello world!");
```

-   컴파일 할 때 어떤 에러가 발생했는지 알려준다.
-   class 파일이 만들어지지 않는다.

<aside>
👩🏻‍💻 참조 : 컴파일러가 하는 일 <br>
<br>
-   구문 체크<br>
-   번역<br>
-   최적화<br>
-   생략된 코드 추가 : `extends Object` 등<br>

</aside>

## 2. 런타임 에러

-   실행 중 발생하는 에러
-   다양한 에러가 발생한다.
-   IDE가 보조하여 알려준다.
-   실행하다 발생하면 프로그램이 종료된다.
-   런타임 에러의 종류 : 에러error와 예외exception
    -   **`error`** : 프로그램 코드에 의해서 수습될 수 없는 심각한 오류 (OutOfMemory error)
    -   **`exception`** : 프로그램 코드에 의해서 수습될 수 없는 다소 미약한 오류
-   에러는 어쩔 수 없지만, 예외는 처리하자.

## 3. 논리적 에러

-   프로그램은 잘 시행이 되나, 의도와 다르게 동작할 때

---

# 🛠️ 예외 처리 exception handling

-   정의 : 프로그램 실행시 발생할 수 잇는 예외 발생에 대비한 코드를 작성하는 것
-   목적 : **프로그램의 비정상 종료**를 막고, 정상적인 실행상태를 유지하는 것

## 예외 클래스의 계층 구조

![](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F8d552bba-31bb-411c-b3b0-652b360a3bd8%2FUntitled.png?id=61097669-fff5-4cfb-b32b-89bdf4ca2909&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1680&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

-   `Throwable` 클래스, 모든 오류의 조상
-   `Exception` 런타임에러 중 미약한 오류
-   `Error` 런타임에러 중 심각한 오류

## RuntimeException 클래스와 그 외 Exception의 자손들
런타임 Exception을 다음과 같이 나누어 볼 수 있다.

-   `RuntimeException` 클래스 외 Exception의 자손들
    -   사용자의 실수와 같은 외적인 요인에 의해 발생하는 예외
    -   예시 : 입출력 예외, 클래스 찾지 못하는 경우
-   `RuntimeException` 클래스와 그 자손들
    -   프로그래머의 실수로 발생하는 예외
    -   예시 : 산술 계산할 때 예외 (5/0), 형변환 예외, nullPoint 예외, IndexOutOfBounds 예외(배열 범위 벗어남)

  
## Exception 종류와 발생 원인

|Exception 종류|발생 원인|
|----------------|---------|
| ClassNotFoundException | 클래스를 발견하지 못함 |
|CloneNotSupportedException|Cloneable 인터페이스 미구현|
|IllegalAccessException|클래스 접근을 못함|
|InstantiationException|추상 클래스나 인터페이스 인스턴화|
| InterruptedException | 쓰레드가 중단 되었을때 |
|NoSuchFieldException|지정된 필드가 없을때 |
| NoSuchMethodException | 지정된 메소드가 없을때 |
| (IOException) CharConversionException | 문자 변환에서 예외가 발생했을때 |
| (IOException) EOFException | 파일의 끝에 도달했을때 |
| (IOException) FileNotFoundException | 파일을 발견하지 않았을 때 |
| (IOException) InterruptedIOException | 입출력 처리가 중단되었을 때 |
| (IOException) (ObjectStreamException) InvalidClassException |클래스 내부의 serialize 처리 문제 발생 |
| (IOException) (ObjectStreamException) InvalidObjectException |  serialize 오브젝트에서 입력 검증 실패 |
| (IOException) (ObjectStreamException) NotActiveException | 스트림 환경이 Active하지 않는데 메소드를 호출한 경우 |
| (IOException) (ObjectStreamException) NotSerializableException | 오브젝트를 serialize할 수 없을 때 |
| (IOException) (ObjectStreamException) OptionalDataException |오브젝트 읽을 때 예상밖의 데이터가 있을 경우 |
| (IOException) (ObjectStreamException) StreamCorruptedException | 읽은 데이터 스트림이 파손되어 있을때 |
| (IOException) (ObjectStreamException) WriteAbortedException | 기록중 예외 발생한 스트림 읽은 경우 
| (IOException) SyncFailedException | FileDescriptor.sync() 호출 실패 시 |
| (IOException) UnsupportedEncodingException | 지정된 문자 부호화 형식 지원안할 때 |
| (IOException) UTFDataFormatException | 부정한 UTF-8방식의 문자열 만날 시 |
| (RuntimeException) ArithmeticException | 제로제산 등의 산술 예외 발생 시 |
| (RuntimeException) ArrayStoreException | 배열에 부정한 형태의 오브젝트 저장 |
| (RuntimeException) (IllegalArgumentException) IllegalThreadStateException | 쓰레드가 요구를 처리하기에는 부적합한 상태일 때 |
| (RuntimeException) (IllegalArgumentException) NumberFormatException | 부적절한 문자열을 수치로 변환할 때 |
| (RuntimeException) IllegalMonitorStateException | 모니터 상태가 부정일때 |
| (RuntimeException) IllegalStateException | 메소드가 요구를 처리하기에는 부적합한 상태일 때 |
| (RuntimeException) (IndexOutOfBoundException) **ArrayIndexOutOfBoundsException** | 범위 밖의 배열 첨자 지정 시 |
| (RuntimeException) (IndexOutOfBoundException) StringIndexOutOfBoundsException | 범위 밖의 String 첨자 지정시 |
| (RuntimeException) NegativeArraySizeException | 배열 크기를 음수로 지정한 경우|
| (RuntimeException) **NullPointerException** | null 오브젝트에 접근한 경우 |
| (RuntimeException) SecurityException| 보안 위반|
| (RuntimeException) UnsupportedOperationException |지원하지 않는 메소드 호출 |

| **Error 종류** | **발생원인** |
|-----------|--------|
| (LinkageError) ClassCircularityError | 클래스 초기화중에 순환 참조를 검출시 |
| (LinkageError) (ClassFormatError) UnsupportedClassVersionError | JVM이 지원되지 않는 버전의 클래스 파일을 읽고자 할때 |
| (LinkageError) ExceptionInInitializerError | 정적 이니셜라이저로 예외가 발생 |
| (LinkageError) (IncompatibleClassChangeError) AbstracMethodError |추상 메소드를 호출했을때 |
| (LinkageError) (IncompatibleClassChangeError) IllegalAccessError | 접근 불가능한 메소드와 필드 사용 시 |
| (LinkageError) (IncompatibleClassChangeError) InstantiationError | 추상클래스나 인터페이스 인스턴스화 |
| (LinkageError) (IncompatibleClassChangeError) NoSuchFieldError | 지정한 필드가 존재하지 않을 때 |
| (LinkageError) (IncompatibleClassChangeError) NoSuchMethodError | 지정한 메소드가 존재하지 않을 때 |
| (LinkageError) NoClassDefFoundError | 클래스 정의가 발견되지 않았을 때 |
| (LinkageError) UnsatisfiedLinkError | 클래스에 포함된 링크 정보를 해결하지 못할 때 |
| (LinkageError) VerifyError | 클래스 파일안에 부적절한 부분이 있을때 |
| ThreadDeath | 쓰레드가 정지해야만 한다는 의미 |
| (VirtualMachineError) InternalError | 내부 에러 |
| (VirtualMachineError) OutOfMemoryError | 메모리부족으로 메모리를 확보 못함 |
| (VirtualMachineError) StackOverflowError | 스택 오버 발생 |
| (VirtualMachineError) UnknownError | 심각한 예외 발생|

---

# 예외 처리 Exception Handling
- 프로그램 실행 시 발생할 수 있는 예외 발생에 대비한 코드를 작성하는 것.
- 프로그램의 비정상 종료를 막고, 정상적인 실행상태를 유지하고자 한다.

## 예외가 주로 발생하는 원인
-   사용자의 잘못된 데이터 입력
-   잘못된 연산
-   개발자가 로직을 잘못 작성
-   하드웨어, 네트워크 오작동
-   시스템 과부하

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

- 주의 : if문과는 달리 `{}`를 생략할 수 없다.

-  try 블럭 내에서 예외가 발생했다면?
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

# 예외 발생시키기
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

### 방법2. Exception 을 상속받아 구현한다.
- `Exception` 은 컴파일 시 발생하는 예외이다.
- 위와 같은 예시에는 컴파일 오류가 발생한다.
	- 아래처럼 try-catch 구문으로 처리하면 컴파일 오류를 막을 수 있다.

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