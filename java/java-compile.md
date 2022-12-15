# Java는 무엇일까?

-   프로그래밍 언어 programing language
-   실행환경(JRE) + 개발도구(JDK) + 라이브러리(API)
-   모던 프로그래밍 언어 (객체지향 언어 + 함수형 언어)

## 주요 특징

1.  객체지향 언어
2.  자동 메모리 관리가 가능하다. (Garbage Collector, GC)
3.  Multi Thread를 지원한다.
4.  풍부한 라이브러리가 존재한다.
5.  **CPU 하드웨어, OS 운영체제 등 플랫폼에 독립적이다.**
    1.  **자바 가상 머신 Java Virtual Machine**

# JVM 자바 가상 머신

-   자바 프로그램이 실행되는 가상 컴퓨터(VM)을 말한다.
-   한 번 작성하면, 어디서든 실행이 가능하다. **Write once, run anywhere**
-   JVM 자체는 하드웨어와 운영체제 위에서 실행되므로 플랫폼에 종속적이다.

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F4c2eec0e-2e87-4538-82ef-50f888b305aa%2FUntitled.png?id=93ded4dc-29f1-4ae9-84c7-0b4fc96548b1&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1680&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

---

# 자바 프로그램의 실행 과정

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F0b79b725-2178-4101-b7e8-fd24c6b01992%2FUntitled.png?id=b91f9b83-d8f1-4819-a74a-b3163f2660bc&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1680&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

![https://err0rcode7.github.io/java/2021/05/16/JVM과자바의실행.html](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F488b6ab7-c950-400c-a358-5b08fa7f276a%2FUntitled.png?id=d5bccc46-ce84-4ac6-ae2f-251b7e9a162a&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1680&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

[참고사항](https://err0rcode7.github.io/java/2021/05/16/JVM%EA%B3%BC%EC%9E%90%EB%B0%94%EC%9D%98%EC%8B%A4%ED%96%89.html)[https://err0rcode7.github.io/java/2021/05/16/JVM과자바의실행.html](https://err0rcode7.github.io/java/2021/05/16/JVM%EA%B3%BC%EC%9E%90%EB%B0%94%EC%9D%98%EC%8B%A4%ED%96%89.html)

## 자바 컴파일러 Java compiler

-   작성한 **소스 코드(.java)** 를 자바 가상 머신이 이해할 수 있는 자바 바이트 코드이자 어플리케이션으로 변환한다. == Compile
-   **.java** → Compile → **.class** → Run → **JVM**

<br>

# 자바 가상 머신 JVM의 구성

1.  자바 인터프리터 interpreter
2.  ****Execution Engine****
    1.  클래스 로더 class loader
    2.  JIT 컴파일러 Just-In-Time compiler
3.  가비지 컬렉터 garbage collector
4.  Runtime Data Area

---

## 1. 자바 인터프리터 interpreter

-   JAVAC 명령으로 자바 프로그램을 중간 형태인 자바 바이트 코드로 컴파일하고, 이를 자바 인터프리터가 한 줄씩 해석하여 기계어로 번역한다.
-   바이트 코드로 쓰여진 파일의 코드를 한 줄씩 읽어내려가면서 실행하는 것이다.

### 🤔 왜 자바는 컴파일과 인터프리터 방식을 병행하는 것인가?

-   컴파일러는 소스코드 전체를 링커등을 통해 한번에 번역하여 기계어 파일로 만들어 메모리상에 적재한다.
    
-   인터프리터는 소스 코드를 한 행씩 중간에 코드로 번역 후 실행한다. (보통 VM)안에서 실행된다.

|  compiler |  interpreter |
|----------|-------------|
|   소스코드 전체를 컴퓨터 프로세서가 실행 할 수 있도록 바로 기계어로 변환 |  고레벨 언어를 중간 코드(intermediate code)로 변환하고 이를 각 행마다 실행. 다른 프로그램에 의해 실행된다. |
|  일반적으로 컴파일러가 실행시간이 빠르다.  | |
| 전체 소스 코드를 변환한 후 에러를 보고한다. | 각 행마다 실행하는 도중 에러가 보고되면 그대로 멈춘다. 보안적인 관점에서 도움 된다. | 
| C, C++ |    Python |


|    자바에서의 compiler 역할     |    자바에서의 interpreter 역할 |
|----------------------------|----------------------------|
|   .java 파일을 .class 파일로 변환한다. (자바 소스코드를 JVM 기계어로 변환) |  자바 컴파일러에 의해 변환된 클래스 파일 내 바이트 코드를 특정 환경 기계에서 실행될 수 있도록 변환한다. ||

-   자바에서는 왜 둘 다 사용할까?    
    -   인터프리팅으로 플랫폼에 종속되지 않는다.
    -   자바 바이트코드는 컴퓨터와 프로그램 사이에 별도 버퍼 역할을 한다.
        -   보안상 도움을 받을 수 있다.
    -   그러나 컴파일러와 인터프리터를 모두 사용하므로 속도가 느리다.

---

## 2-1. 클래스 로더 class loader

![https://dailyheumsi.tistory.com/196](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ff80246f6-0c59-45df-9417-c306d128a81f%2FUntitled.png?id=bd093800-c799-46f4-9310-05a227626478&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1680&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

[참조](https://dailyheumsi.tistory.com/196)

-   자바는 동적 로드 (바이트 코드를 실행하는 런타임)에서 클래스를 로드하고 링크하는 특징이 있다.
-   클래스 로더는 런타임 중 JVM의 메소드 영역에 동적으로 Java 클래스를 로드하는 역할을 한다.
-   로딩, 링크, 초기화 단계로 나뉘어져 있다.

---

### 단계 : 1.로딩

1.  자바 바이트 코드를 읽고 그 내용에 따라 **바이너리 데이터**를 만들고 메서드 영역(Method Area)에 저장한다.
2.  저장하는 내용
    1.  로드된 클래스를 비롯한 그의 부모 클래스 정보
    2.  클래스 파일과 Class, Interface, Enum 관련 여부를 구분하여 저장
    3.  변수나 메서드 정보
3.  이 과정에서 `.class` 파일이 JVM 스펙에 맞는지, Java 버전이 맞는지 확인한다.
4.  로딩이 끝나면 해당 클래스 타입의 객체를 생성하여 메모리의 힙 영역(Heap Area)에 저장한다.


### 단계 : 2.링크

-   검증 Verify
    -   읽어 들인 클래스가 자바 언어 명세 및 JVM 명세에 명시된 대로 잘 구성되어 있는지 (유효한지) 검사한다.
    -   설정에 따라 성능 향상을 위해 진행하지 않도록 설정 가능하다.
-   준비 Prepare
    -   클래스가 필요로 하는 메모리를 할당하고, 클래스에서 정의된 필드, 메소드, 인터페이스를 나타내는 데이터 구조를 준비한다.
    -   static 변수, 기본값에 필요한 메모리 공간을 준비한다.
-   분석 Resolution
    -   심볼릭 메모리 레퍼런스를 메소드 영역에 있는 실제 레퍼런스로 교체한다. 다이렉트 레퍼런스, 즉 실제 메모리 주소 값으로 변경해주는 작업을 한다.


### 단계 : 3.초기화

-   링크-Prepare 단계에서 확보한 메모리 영역에 클래스 변수들을 적절한 값으로 초기화 한다. 즉, static 필드들이 설정된 값으로 초기화한다.
-   SuperClass 초기화와 해당 클래스의 초기화를 진행한다.

---

### 구조

-   클래스 로더는 계층 구조로 이루어져 있다.
-   기본적으로 3가지 클래스 로더가 제공된다.
-   개발자 필요에 따라 커스텀 클래스 로더를 구현할 수 있다.


### 구조 : 1. Bootstrap ClassLoader

-   최상위 우선순위를 갖는 클래스 로더. JVM 시작시 가장 최초로 실행되는 클래스 로더.
-   자바 자체의 클래스 로더와 최소한의 자바 클래스만을 로드한다.
    -   java.lang.Object
    -   Class, ClassLoader
    -   Java 8 : `jre/lib/rt.jar` 를 로드한다.
    -   Java 9 ~ : 더이상 `/rt.jar`가 존재하지 않고, `/lib` 내에 모듈화되어 포함되었다. 이제는 ClassLoader 내 최상위 클래스들만 로드한다.
-   네이티브 코드로 구현되어 있다.


### 구조 : 2. Extension ClassLoader → Platform ClassLoader

-   확장 클래스 로더는 부트스트랩 클래스로더를 부모로 갖는 클래스 로더이다.
-   확장 자바클래스들을 로드한다.
-   java.ext.dirs 환경변수에 설정된 디렉토리의 클래스 파일을 로드하고 이 값이 설정되어 있지 않은 경우 `${JAVA_HOME}/jre/lib/ext` 에 있는 클래스 파일을 로드한다.
    -   java 8 : `URLClassLoader` 를 상속. `jre/lib/ext` 내 모든 클래스 로드
    -   java 9 ~ : Platform Loader로 변경되었으며, URLClassLoader가 아닌 `BuiltinClassLoader`를 상속한다. Inner Static 클래스로 구현되어 있다.


### 구조 : 3. System ClassLoader

-   자바 프로그램 실행시 지정한 ClassPath에 있는 클래스 파일 혹은 jar에 속한 클래스들을 로드한다. == `.class` 확장자 파일을 로드한다.
-   개발자가 애플리케이션 구동을 위해 직접 작성한 대부분의 클래스는 여기서 로딩된다.
-   Java 8 : Application ClassLoader로 불림.
-   Java 9~ : 클래스패스, 모듈패스에 있는 클래스 로딩.
-   `URLClassLoader`를 상속받아`ClassLoaders` 클래스의 내부 static 클래스로 구현됨

---

### 원칙 : 1. ****Delegation Principle****

![https://homoefficio.github.io/2018/10/13/Java-클래스로더-훑어보기/](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fa1f5eb81-3e38-4582-8ec6-a364ae8d48d2%2FUntitled.png?id=2156fe20-3644-462f-b517-8f0cce4b7828&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1680&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

[참조 : https://homoefficio.github.io/2018/10/13/Java-클래스로더-훑어보기/](https://homoefficio.github.io/2018/10/13/Java-%ED%81%B4%EB%9E%98%EC%8A%A4%EB%A1%9C%EB%8D%94-%ED%9B%91%EC%96%B4%EB%B3%B4%EA%B8%B0/)

-   **위임 원칙**은 클래스 로딩이 필요할 때 **3가지 기본 클래스로더의 윗 방향으로 클래스 로딩을 위임하는 것**을 말한다.

### 원칙 : 2. ****Visibility Principle****

-   **가시범위 원칙**은 **하위 클래스로더는 상위 클래스로더가 로딩한 클래스를 볼 수 있지만, 상위 클래스로더는 하위 클래스로더가 로딩한 클래스를 볼 수 없다**는 원칙이다.

### 원칙 : 3. ****Uniqueness Principle****

-   **유일성 원칙**은 **하위 클래스로더는 상위 클래스로더가 로딩한 클래스를 다시 로딩하지 않게 해서 로딩된 클래스의 유일성을 보장**한다.
-   유일성을 식별하는 기준은 클래스의 `**binary name**`인데, `toString()`으로 찍다보면 가끔 보이는 `java.lang.String`, `javax.swing.JSpinner$DefaultEditor`, `java.security.KeyStore$Builder$FileBuilder$1`, `java.net.URLClassLoader$3$1` 이런 것들이 바로 `binary name`이다.

---

## 2-2. JIT 컴파일러 Just-In-Time compiler

-   JIT컴파일러는 인터프리터의 단점을 보완한다.
-   JIT(Just-In-Time) 컴파일러는 런타임 시 바이트 코드를 원시 시스템 코드로 컴파일하여 Java 애플리케이션의 성능을 향상시키는 런타임 환경의 컴포넌트이다.
-   JIT 컴파일러는 처음 바이트 코드를 읽을 때에는 인터프리터 방식으로 한줄 한줄 씩 읽고 반복되는 바이트 코드를 또 읽게되면 캐싱해둔 곳에서 native code(원시코드)로 컴파일한다.
-   변환된 원시코드는 인터프리터의 변환과정없이 직접적으로 사용이 가능하며(기존에는 바이트코드에서 원시코드로 변환 후 실행하였다면 JIT 컴파일러를 사용하여 변환된 원시코드는 변환하지않고 바로 실행) 이로 인해 시스템의 성능이 좋아지게 된다.
-   [JIT 컴파일러의 코드 최적화 방법 참고링크](https://www.ibm.com/docs/ko/sdk-java-technology/8?topic=compiler-how-jit-optimizes-code)

---

## 3. Garbage Collector

-   Garbage Collector는 Heap 메모리 영역에 생성된 객체들 중에 참조되지 않은 객체들을 제거하는 역할을 한다.
-   [동작원리 참고 링크](https://err0rcode7.github.io/java/2021/05/12/%EA%B0%80%EB%B9%84%EC%A7%80%EC%BB%AC%EB%A0%89%EC%85%98.html)

---

## 4. ****Runtime Data Area****

![https://steady-snail.tistory.com/67](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F59b15412-dddd-4e22-91f7-9fc4c6a69400%2FUntitled.png?table=block&id=74673b98-97ae-4692-a5a7-891b0b0fe4c4&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1680&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

[](https://steady-snail.tistory.com/67)[https://steady-snail.tistory.com/67](https://steady-snail.tistory.com/67)

-   JVM의 메모리 영역으로 Java 애플리케이션 실행시 사용되는 데이터를 적재하는 영역이다.
-   구분
    -   PC register
    -   Stack
    -   Native Method Stack
    -   Heap
    -   Method Area

### PC register

-   스래드가 생성될때마다 생성되는 영역으로 Program Counter 즉, 현재 쓰레드가 실행되는 부분의 주소와 명령을 저장하고 있는 영역이다. 이것을 이용해서 여러 쓰레드를 제어한다.
-   JVM은 Stacks-Base 방식으로 작동한다. CPU에 직접 Instruction을 수행하지 않고 Stack에서 Operand를 뽑아내 이를 별도의 메모리 공간에 저장하는 방식을 취한다. 이러한 메모리 공간을 PC register라고 한다.

### Stack

-   지역 변수, 파라미터, 리턴 값, 연산에 사용되는 임시 값등이 생성되는 영역이다.
-   `int x = 10;` 이라는 소스를 작성했다면 정수값이 할당될 수 있는 메모리공간을 x라고 잡아두고 그 메모리 영역에 값이 10이 들어간다. 즉, 스택에 메모리에 이름이 x라고 붙여주고 값이 10인 메모리 공간을 만든다.
-   `Animal dog = new Animal();` 이라는 코드를 작성했다면 Animal dog은 스택 영역에 생성되고 new로 생성된 Animal클래스의 인스턴스는 힙 영역에 생성된다.
-   스택영역에 생성된 dog의 값으로 힙 영역의 주소값을 가지고 있다. 즉 스택 영역에 생성된 dog가 힙 영역에 생성된 객체를 참조하고 있는 것이다.

### Native Method Stack

-   자바 외 언어로 작성된 네이티브 코드를 위한 메모리 영역이다. 보통 C/C++ 등의 코드를 수행하기 위한 스택이다.
-   JNI를 통해 표준에 가까운 방식으로 구현이 가능하다.

### Heap

-   인스턴스화 된 모든 클래스 인스턴스와 배열을 저장을 하는 공간이다.
-   모든 JVM 스레드에 공유되는 공유 자원이기도 하다.
-   Heap에 저장된 할당된 메모리 회수 권한은 무조건 가비지 컬렉터에 의해서만 회수가 가능하다.

### Method Area

-   클래스 수준의 정보를 저장하는 공간이다.
    -   타입 정보 (Interface, class)
    -   필드 정보(클래스 멤버 변수의 이름, 데이터 타입, 접근 제어자 정보)
    -   메서드 정보(메소드의 이름, 리턴 타입, 파라미터, 접근 제어자 정보)
    -   런타임 상수 풀(상수 풀 : 문자 상수, 타입, 필드, 객체 참조)
    -   static 변수, final class 등
    -   클래스 변수
-   모든 JVM 스레드에 공유되는 공유 자원이다.
-   사실 논리적으로 Heap 영역에 포함되는 영역이다.
-   객체 생성 후에 메소드를 실행하게 되면 해당 클래스 코드에 대한 정보를 Method Area에 저장 하게 된다.

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F0504d8a8-5fe2-4e7c-9d51-12c46b6312b3%2FUntitled.jpeg?table=block&id=ab0e1a52-5c2f-44f6-a716-9e916d936a95&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1680&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

---

-   참고
    -   [자바 프로그램의 실행 과정](http://www.tcpschool.com/java/java_intro_programming)
    -   자바의 정석 Chapter 1
    -   [JVM 동작원리 및 기본개념](https://steady-snail.tistory.com/67)
    -   [Java는 왜 컴파일러와 인터프리터 둘 다 가지는가?](https://velog.io/@tsi0521/Java%EB%8A%94-%EC%BB%B4%ED%8C%8C%EC%9D%BC%EB%9F%AC%EC%99%80-%EC%9D%B8%ED%84%B0%ED%94%84%EB%A6%AC%ED%84%B0-%EB%91%98-%EB%8B%A4-%EA%B0%80%EC%A7%84%EB%8B%A4)
    -   [Java URLClassLoader로 알아보는 클래스로딩](https://homoefficio.github.io/2018/10/14/Java-URLClassLoader%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-%ED%81%B4%EB%9E%98%EC%8A%A4%EB%A1%9C%EB%94%A9/)
    -   [클래스로더 훑어보기](https://homoefficio.github.io/2018/10/13/Java-%ED%81%B4%EB%9E%98%EC%8A%A4%EB%A1%9C%EB%8D%94-%ED%9B%91%EC%96%B4%EB%B3%B4%EA%B8%B0/)