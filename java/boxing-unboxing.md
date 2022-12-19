## 오토 박싱 & 오토 언박싱

> 자바에는 기본 타입(primitive type)과 Wrapper 클래스가 존재한다.

- 기본 타입 (primitive type) : stack 에 값을 저장
    - 정수 타입(byte, short, int, long)
    - 소수 타입(float, double)
    - bool 타입(boolean)
    - 문자 타입(char)
- Wrapper 클래스 : stack 에 주소를 저장하고 heap 에서 값을 참조
    - 정수 타입(Byte, Short, Integer, Long)
    - 소수 타입(Float, Double)
    - bool 타입(Boolean)
    - 문자 타입(Character)
    - `값 비교`에는 `equals`를 사용합니다. `==`는 인스턴스의 `주소비교`에 사용

![](https://velog.velcdn.com/images/ummchicken/post/9a54d71f-e59f-41b9-b26d-f4ae69127ddb/image.png)

박싱과 언박싱에 대한 개념을 먼저 살펴보자

## 박싱

> 기본 타입 데이터에 대응하는 Wrapper 클래스로 만드는 동작 (Primitive -> Wrapper)

```java
// 박싱
int i = 10;
Integer num = new Integer(i);
```

- 명시적인 박싱 : 프로그래머가 코딩하여 **명시적으로 wrapper로 변환**하는 것 (직접 타입변환을 기재하는 경우)
```java
int intData = 512;

// 명시적인 방식
Integer integerData = (Integer)intData;
```

<br>

- 묵시적인 박싱 : 프로그래머가 임의로 박싱을 해주는 것이 아니라 **자동으로 박싱**이 되는 것
```java
int intData = 512;
 
// 묵시적인 방식
Integer integerData = intData;
```

<br>

## 언박싱

> Wrapper 클래스에서 기본 타입으로 변환 (Wrapper -> Primitive)

```java
// 언박싱
Integer num = new Integer(10);
int i = num.intValue();
```

- 명시적인 언박싱 : 프로그래머가 코딩하여 **명시적으로 primitive로 변환**하는 것 (**Auto**)
```java
int intData = 512;

// 명시적인 언방식
int sum = (int)integerData + 100;
System.out.println(sum);
```

<br>

- 묵시적인 언방식 : 코드상 프로그래머가 임의로 언박싱을 하는 것이 아니라 **자동으로 언박싱**이 되는 현상
```java
int intData = 512;

// 묵시적인 언방식
int sum = integerData + 100;
System.out.println(sum);
```

<br>

### Boxing / Unboxing 성능 고려 요소

→ Java에서 아무리 기능적 편의성을 위하여 박싱과 언박싱 그리고 오토박싱을 제공하지만, 
명백히 다른 타입 간의 형변환은 **어플리케이션의 성능**에 영향을 미칠 수 밖에 없다.

<br>

예제

- **Auto Boxing**을 포함한 연산
```java
public static void main(String[] args) {
  long t = System.currentTimeMillis();
  Long sum = 0L;

  for (long i = 0; i < 1000000; i++) {
  	sum += i;
  }

  System.out.println("processing time: " + (System.currentTimeMillis() - t) + " ms") ;
}

// processing time: 21 ms
```

<br>

- **동일 primitive 타입**간 연산
```java
public static void main(String[] args) {
    long t = System.currentTimeMillis();
    long sum = 0L;

    for (long i = 0; i < 1000000; i++) {
        sum += i;
    }

    System.out.println("processing time: " + (System.currentTimeMillis() - t) + " ms") ;
}

// processing time: 4 ms
```

→ 총 100만번의 sum 연산을 통해 대략 5배의 결과차이를 보이는 것으로 확인했다. 
100만건의 결과는 서비스 어플리케이션에서는 결코 작은 숫자는 아닐 것

→ 따라서 작성한 코드에 불필요한 **auto casting**이 반복적으로 이루어지고 있는지 확인하는 것은 
대용량 서비스를 개발하는데 있어서 필수적으로 파악해야하는 요소임

<br>

---

## 출처

- [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Language/[Java] Auto Boxing %26 Unboxing.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Language/%5BJava%5D%20Auto%20Boxing%20%26%20Unboxing.md)
- [https://ktko.tistory.com/entry/자바-박싱boxing과-언박싱unboxing](https://ktko.tistory.com/entry/%EC%9E%90%EB%B0%94-%EB%B0%95%EC%8B%B1boxing%EA%B3%BC-%EC%96%B8%EB%B0%95%EC%8B%B1unboxing)
- [https://sas-study.tistory.com/407](https://sas-study.tistory.com/407)
- [https://velog.io/@skyepodium/자바-박싱-언박싱은-낯설어서](https://velog.io/@skyepodium/%EC%9E%90%EB%B0%94-%EB%B0%95%EC%8B%B1-%EC%96%B8%EB%B0%95%EC%8B%B1%EC%9D%80-%EB%82%AF%EC%84%A4%EC%96%B4%EC%84%9C)