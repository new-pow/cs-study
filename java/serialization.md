## 직렬화(Serialization)란?

> 자바 시스템 내부에서 사용되는 객체(Object) 또는 데이터(Data)를  
외부의 자바 시스템에서도 사용할 수 있도록 바이트(byte) 형태로 데이터 변환하는 기술

```※ 쉬운 설명  
  
● 데이터 직렬화  
→ 메모리를 디스크에 저장하거나, 네트워크 통신에 사용하기 위한 형식으로 변환하는 것  
(자바의 객체를 바이트의 배열(byte\[\])로 변환)  
  
● 데이터 역직렬화  
→ 디스크에 저장한 데이터를 읽거나,  
네트워크 통신으로 받은 데이터를 메모리에 쓸 수 있도록 변환하는 것  
(저장된 것을 다시 객체(Object)로 변화)
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fp4IoA%2FbtrUtGU7m4Y%2FUC9oHUZu9AlZfWbmhTa4Tk%2Fimg.png)

## 직렬화를 하는 이유?

→ 직렬화가 된 데이터는 언어에 따라서 텍스트 또는 바이너리 등의 형태가 되는데,

이는 파일 저장이나 네트워크 전송 시 파싱이 가능한 유의미한 데이터가 된다.

따라서, 전송 및 저장이 가능한 데이터로 만들어주는 것이 바로 '**직렬화(Serialization)**'이라고 말할 수 있다.

<br>

\+ 추가

각자 PC의 OS마다 서로 다른 가상 메모리 주소 공간을 갖기 때문에,

Reference Type(참조 타입)의 데이터들은 인스턴스를 전달 할 수 없다.

따라서, 이런 문제를 해결하기 위해선

주소값이 아닌 Byte 형태로 직렬화된 객체 데이터를 전달해야 한다.

<br>

※ 참고

개발 언어를 무엇을 선택하든, 사용하는 데이터의 메모리 구조는 크게 2가지로 나뉜다.

-   값 형식(Value Type) 데이터
    -   int, float, char 등 값 형식 데이터는 스택에 메모리가 쌓이고 직접 접근이 가능하다.
-   참조 형식(Reference Type) 데이터
    -   객체와 같은 참조 형식 변수를 선언하면 힙에 메모리가 할당되고, 스택에서는 이 힙 메모리를 참조하는 구조로 되어 있다.

<br>

---

<br>

## 직렬화

### 직렬화(Serialize) 조건

> **java.io.Serializable** 인터페이스를 구현해야 한다.

<br>

**직렬화 대상** : 인터페이스 상속 받은 객체, Primitive 타입의 데이터.

Primitive 타입이 아닌 Reference 타입처럼 주소값을 지닌 객체들은

바이트로 변환하기 위해 Serializable 인터페이스를 구현해야 한다.

```
public class Member implements Serializable {
    private String name;
    private String email;
    private int age;

    public Member(String name, String email, int age) {
        this.name = name;
        this.email = email;
        this.age = age;
    }
    
    @Override
    public String toString() {
        return String.format("Member{name='%s', email='%s', age='%s'}", name, email, age);
    }
}
```

<br>

### 직렬화 방법

> **java.io.ObjectOutputStream**를 사용하여 직렬화를 진행

<br>

#### 단계 1. serialVersionUID를 만들어준다.

```
@Entity
@AllArgsConstructor
@toString
public class Post implements Serializable {
private static final long serialVersionUID = 1L;
    
private String title;
private String content;
```

※ serialVersionUID 밑에서 설명

<br>

#### 단계 2. **ObjectOutputStream**으로 직렬화를 진행한다. Byte로 변환된 값을 저장하면 된다.

```
Post post = new Post("제목", "내용");
byte[] serializedPost;
try (ByteArrayOutputStream baos = new ByteArrayOutputStream()) {
    try (ObjectOutputStream oos = new ObjectOutputStream(baos)) {
        oos.writeObject(post);

        serializedPost = baos.toByteArray();
    }
}
```

<br>

---

## 역직렬화

<br>

### 역직렬화(Deserialize) 조건

> 직렬화 대상이 된 객체의 클래스가 class path에 존재해야 하며 import되어 있어야 한다.

<br>

※ class path란?

→ JVM이 프로그램을 실행할 때, class 파일을 찾는 데 기준이 되는 파일 경로

<br>

자바 직렬화 대상 객체는 동일한 **serialVersionID**를 가지고 있어야 한다.

→ 예) **private static final long serialVersionUID = 1L;**

<br>

**serialVersionUID**이 왜 필요한지 자세한 내용은 아래에 추가.

<br>
<br>

### 역직렬화 방법

> **java.io.ObjectInputStream**를 사용하여 역직렬화를 진행

<br>

#### **ObjectInputStream**로 역직렬화를 진행한다. Byte의 값을 다시 객체로 저장하는 과정

```
// 직렬화 예제에서 생성된 serializedPost 데이터
try (ByteArrayInputStream bais = new ByteArrayInputStream(serializedPost)) {
    try (ObjectInputStream ois = new ObjectInputStream(bais)) {

	// 역직렬화된 Post 객체를 읽어온다.
        Object objectPost = ois.readObject();
        Post post = (Post) objectPost;
    }
}
```

<br>

---

<br>

## 직렬화 serialVersionUID

<br>

위의 코드에서 serialVersionUID를 직접 설정했었다.

사실 선언하지 않아도, 자동으로 해시값이 할당된다.

<br>

**직접 설정한 이유**

→ 기존의 클래스 멤버 변수가 변경되면 serialVersionUID가 달라지는데,

역직렬화 시 달라진 넘버로 Exception이 발생될 수 있다.

<br>

따라서 직접 serialVersionUID을 관리해야

클래스의 변수가 변경되어도 직렬화에 문제가 발생하지 않게 된다.

<br>

#### **또 다른 문제...**

String \-> StringBuilder, int \-> long으로 변경해도 역직렬화에서 Exception이 발생.

→ 자바 직렬화는 상당히 타입의 엄격하다는 것을 알 수 있음.

역직렬화 대상의 클래스의 멤버 변수 타입 변경을 지양해야 한다.

<br>

serialVersionUID을 관리하더라도,

멤버 변수의 타입이 다르거나, 제거 혹은 변수명을 바꾸게 되면

Exception은 발생하지 않지만 데이터가 누락될 수 있음.

→ 멤버 변수가 빠지게 된다면 Exception 대신 null값이 들어간다.

(serialVersionUID의 값이 동일하면 멤버 변수 및 메소드 추가는 문제되지 않는다.

→ 추가된 멤버 변수 및 메소드의 데이터는 누락된다.)

<br>

---

<br>

## 다른 Format의 직렬화

> 직렬화방법에는 여러 Format이 존재

<br>

**CSV형태**

→ 표형태의 다량의 데이터를 직렬화

<br>

**XML, JSON형태**

→ 구조적인 데이터

<br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcUc2xk%2FbtrUtiG0dGp%2FcPFoMalrRfydmqE3oSO9lk%2Fimg.png)

<br>

### CSV

> 데이터를 표현하는 가장 많이 사용되는 방법 중 하나로 콤마(,) 기준으로 데이터를 구분하는 방법

예) nesoy,youngjaeKwon,Seoul,Korea -> \[nesoy, youngjaeKwon, Seoul, Korea\]

```
Member member = new Member("김배민", "deliverykim@baemin.com", 25);
// member객체를 csv로 변환
String csv = String.format("%s,%s,%d",member.getName(), member.getEmail(), member.getAge());
System.out.println(csv);
```

<br>

### JSON

```
Member member = new Member("김배민", "deliverykim@baemin.com", 25);
// member객체를 json으로 변환
String json = String.format(
        "{\"name\":\"%s\",\"email\":\"%s\",\"age\":%d}",
        member.getName(), member.getEmail(), member.getAge());
System.out.println(json);
```

<br>

---

<br>

## 자바의 직렬화 왜 사용하는가?

-   복잡한 데이터 구조의 클래스의 객체라도 직렬화 기본 조건만 지키면 큰 작업 없이 바로 직렬화, 역직렬화가 가능.
-   데이터 타입이 자동으로 맞춰지기 때문에 관련 부분을 큰 신경을 쓰지 않아도 됨.

<br>

## 어디에 사용되는가? (직렬화 상황)

#### 서블릿 세션 (Servlet Session)

```
세션을 서블릿 메모리 위에서 운용한다면 직렬화를 필요로 하지 않지만,  
파일로 저장하거나 세션 클러스터링, DB를 저장하는 옵션 등을 선택하게 되면  
세션 자체가 직렬화가 되어 저장되어 전달된다.
```

<br>

#### 캐시 (Cache)

```Ehcache, Redis, Memcached 라이브러리 시스템을 많이 사용된다.```

<br>

#### 자바 RMI(Remote Method Invocation)

```원격 시스템 간의 메시지 교환을 위해서 사용하는 자바에서 지원하는 기술```

<br>

---

<br>

## 요약

-   데이터를 통신 상에서 전송 및 저장하기 위해 직렬화/역직렬화를 사용한다.
-   **serialVersionUID**는 개발자가 직접 관리한다.
-   클래스 변경을 개발자가 예측할 수 없을 때는 직렬화 사용을 지양한다.
-   개발자가 직접 컨트롤 할 수 없는 클래스(라이브러리 등)는 직렬화 사용을 지양한다.
-   자주 변경되는 클래스는 직렬화 사용을 지양한다.
-   역직렬화에 실패하는 상황에 대한 예외처리는 필수로 구현한다.
-   직렬화 데이터는 타입, 클래스 메타정보를 포함하므로 사이즈가 크다. 트래픽에 따라 비용 증가 문제가 발생할 수 있기 때문에 JSON 포맷으로 변경하는 것이 좋다. (JSON 포맷이 직렬화 데이터 포맷보다 2~10배 더 효율적)

<br>

---

<br>

### 출처

-   [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Language/%5BJava%5D%20%EC%A7%81%EB%A0%AC%ED%99%94(Serialization).md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Language/%5BJava%5D%20%EC%A7%81%EB%A0%AC%ED%99%94(Serialization).md)
-   [https://steady-coding.tistory.com/576](https://steady-coding.tistory.com/576)
-   [https://nesoy.github.io/articles/2018-04/Java-Serialize](https://nesoy.github.io/articles/2018-04/Java-Serialize)
-   [https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=kkson50&logNo=220564174258](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=kkson50&logNo=220564174258)
-   [https://n1tjrgns.tistory.com/259](https://n1tjrgns.tistory.com/259)