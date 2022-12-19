# String, StringBuffer, StringBuilder

| 분류 | String | StringBuffer | StringBuilder |
| --- | --- | --- | --- |
| 변경 | Immutable (불변) | Mutable (가변) | Mutable |
| 동기화 |  | Synchronized 가능 (Thread-safe) | Synchronized 불가능 |

<br>

## 1. String 클래스의 특징 (객체 생성 방법에 따른 차이)

> String은 기본형(int, floa, char 등)과는 다르고, 첫 글자가 대문자로 시작하는 **클래스**이다.
> 

<br>

### 1. new 연산을 통해 생성된 인스턴스의 메모리 공간은 변하지 않음 (Immutable)

> 값이 같은 String은 String Pool 내에서 String 객체를 공유
> 

```java
// 1. 
String s1 = "Hello";

// 2. 
String s2 = "Hello";

// 3. 
String s3 = new String("Hello");

// 4. 
String s4 = new String("Hello");
```

💡 먼저, **s1과 s2처럼 문자열로 생성된 String 객체**는 해당 문자열이 동일한 경우, 그 문자열을 공유한다. 따라서 비교연산자(==)로 참조변수 s1과 s2를 비교하게 되면, 결과가 true로 나온다.


💡 반면, **s3와 s4처럼 new 연산자를 통해 String 객체를 생성**하게 되면, 해당 문자열이 동일한 내용일지라도 각 객체마다 문자열이 새롭게 생성된다. 따라서 비교연산자(==)로 참조변수 s3과 s4를 비교하게 되면, 각 변수가 가리키고 있는 주소값이 다르기 때문에 결과는 false로 나온다.

![](https://velog.velcdn.com/images/ummchicken/post/c5a42da7-005d-4ca8-9148-49a6ab5f62dd/image.png)

→ 따라서 문자열의 경우 String이 클래스이지만, new 연산자로 생성하는 것보다 문자열 대입을 통해 생성하는 것이 좋다.

- 추가 그림
    - String 을 리터럴 값으로 할당하는 경우
    
    ```java
    String strA = "abc";
    String strC = "abc";
    ```
    
    ![](https://velog.velcdn.com/images/ummchicken/post/79f61267-3fe1-4e41-80da-0a6492988fbd/image.png)

    
    - new 키워드로 값을 할당하는 경우
    
    ```java
    String strB = new String("abc");
    String strD = new String("abc");
    ```
    
    ![](https://velog.velcdn.com/images/ummchicken/post/638b8af8-3318-4998-9daa-c40f520e9fe1/image.png)

<br>


### 2. String 객체는 내용을 수정할 수 없는 immutable 클래스

> String 객체를 한번 생성하고 나면, 그 객체의 내용은 수정할 수 없다.
> 

![](https://velog.velcdn.com/images/ummchicken/post/12b92d9d-aad7-4c5b-b1f0-1a8623297435/image.png)

- 그림 설명
    “Hello” 문자열 객체를 만든 후 다시 “World” 문자열을 더하게 되면, 
    “Hello” 문자열 객체가 “HelloWorld”로 바뀌는 것이 아니라 
    “Hello” 객체는 그대로 있고, 새롭게 “HelloWorld” 객체가 생성된다.
    그리고 참조변수 s1은 새롭게 생성된 문자열 “HelloWorld”을 가리키도록 변경된다.
    
→ 그런데 만약, 자주 문자열 내용을 변경하게 되면 그림과 같이 새로운 문자열이 계속 생기게 되므로 효율이 떨어진다. 
→ 그래서 문자열 내용을 수정할 수 있는 클래스로 StringBuffer 클래스가 있다. 

<br>

### 3. 객체가 불변하므로, Multithread에서 동기화를 신경 쓸 필요가 없음. (조회 연산에 매우 큰 장점)

> 객체가 불변이면 멀티 스레드 환경에서도 값이 바뀔 위험이 없다.

- 자연스럽게 **thread-safe**한 특성을 갖게 됨
- 동기화와 관련된 위험 요소에서 벗어날 수 있음
- 여러 스레드에서 동시에 접근해도 별다른 문제가 없음
- 또한 String의 경우 한 스레드에서 값을 바꾸면, 해당 객체의 값을 수정하는 것이 아니라 새로운 객체를 String Pool에 생성한다. 따라서 **thread-safe**하다고 볼 수 있다.

### 4. Garbage Collector로 제거되어야 함

![](https://velog.velcdn.com/images/ummchicken/post/e39ec39c-4e12-4845-bc6a-e1726641f124/image.png)

<br>

### String을 사용해야 할 때

- 짧은 문자열을 더할 경우
- 문자열 연산이 적고 멀티스레드 환경일 경우

---

## **2. StringBuffer, StringBuilder 특징**

> String과 다르게 동작함. **Stringbuilder**나 **StringBuffer** 객체는 한번 값이 할당되더라도 한번 더 다른 값이 할당되면 할당된 공간이 변하는 특성을 가짐.

<br>

### 공통점

1. new 연산으로 클래스를 한 번만 만듬 (Mutable)
2. 문자열 연산시 새로 객체를 만들지 않고, 크기를 변경시킴
(내부동작을 통해 값이 변경되더라도 **같은 주소공간을 참조**하게 되는 것, **값이 변경되는 가변성**)
3. StringBuffer와 StringBuilder 클래스의 메서드가 동일함

<br>

### 차이점

> 동기화 여부

- StringBuffer는 메서드에서 `synchronized` 키워드를 사용
- `synchronized` 란?
  - 공유 데이터에 lock을 걸어 작업중이던 쓰레드가 마칠때까지 다른 쓰레드에게 제어권이 넘어가지 않게 보호한다.
  - Synchronized 블럭이 끝나면 lock이 풀리고 다른 쓰레드도 접근 가능하게 된다.
    
- 예제
`멀티스레드 환경에서 A 스레드와 B스레드 모두 같은 StringBuffer 클래스 객체 sb의 append() 메서드를 사용하려고 하면`
    - **A 스레드** : sb의 append() 동기화 블록에 접근 및 실행
    - **B 스레드** : A 스레드 sb 의 append() 동기화 블록에 들어가지 못하고 block 상태가 됨.
    - **A 스레드** : sb의 append() 동기화 블록에서 탈출
    - **B 스레드** : block 에서 running 상태가 되며 sb 의 append() 동기화 블록에 접근 및 실행.

<br>

### **StringBuilder 를 사용 해야 할 때**

> **StringBuilder**는 동기화를 지원하지 않는 반면, 속도면에선 StringBuffer 보다 성능이 좋다.

- 문자열 연산이 많고 **단일스레드**이거나 동기화를 고려하지 않아도 되는 경우
- 스레드에 안전한지 여부가 전혀 관계 없는 프로그램을 개발할 경우

<br>

### **StringBuffer 를 사용해야 할 때**

> **StringBuffer**는 동기화를 지원하여 멀티 스레드 환경에서도 안전하게 동작할 수 있다.

- 문자열 연산이 많고 **멀티스레드 환경**일 경우
- 스레드에 안전한 프로그램이 필요할 때나, 개발 중인 시스템의 부분이 스레드에 안전한지 모를 경우

<br>

### 속도 비교

3개의 성능을 비교해보면 `StringBuilder > StringBuffer > String` 순으로 StringBuilder가 제일 빠름

---

## 출처

- [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Language/[java] String StringBuilder StringBuffer 차이.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Language/%5Bjava%5D%20String%20StringBuilder%20StringBuffer%20%EC%B0%A8%EC%9D%B4.md)
- [https://kadosholy.tistory.com/109](https://kadosholy.tistory.com/109)
- [https://starkying.tistory.com/entry/why-java-string-is-immutable](https://starkying.tistory.com/entry/why-java-string-is-immutable)
- [https://velog.io/@heoseungyeon/StringBuilder와-StringBuffer는-무슨-차이가-있는가](https://velog.io/@heoseungyeon/StringBuilder%EC%99%80-StringBuffer%EB%8A%94-%EB%AC%B4%EC%8A%A8-%EC%B0%A8%EC%9D%B4%EA%B0%80-%EC%9E%88%EB%8A%94%EA%B0%80)
- [https://dejavuhyo.github.io/posts/string-stringbuffer-stringbuilder/](https://dejavuhyo.github.io/posts/string-stringbuffer-stringbuilder/)
- [https://crosstheline.tistory.com/72](https://crosstheline.tistory.com/72)