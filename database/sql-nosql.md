기본적으로 두 기술의 가장 큰 차이점은 

### SQL은 관계형 데이터베이스이고, 

### NoSQL은 비관계형 데이터베이스이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcIaP9g%2FbtrVpud400Q%2FDtv1KzrKDeWKwYbGLbxBYK%2Fimg.png)

보통 Spring에서 개발할 때는 MySQL을, 

Node.js에서는 MongoDB를 주로 사용했을 것이다.

하지만 그냥 단순히 프레임워크에 따라 결정하는 것이 아니다.

프로젝트를 진행하기에 앞서 적합한 데이터베이스를 택해야 한다.

차이점을 알아보자.

---

## SQL (관계형 DB)

SQL을 사용하면 RDBMS(관계형 DB 관리 시스템)에서 데이터를 저장, 수정, 삭제 및 검색할 수 있다.

주로 데이터의 다양한 엔티티와 변수 간의 관계가 있는 구조화된 데이터를 관리하는 데 사용된다.

관계형 데이터베이스에는 핵심적인 두 가지 특징이 있다.

1.  데이터는 **정해진 데이터 스키마에 따라 테이블에 저장**된다.
2.  데이터는 **관계를 통해 여러 테이블에 분산**된다.

#### **엄격한 스키마**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbjlzWw%2FbtrVjRax8iQ%2FkC0X7No0xUvXNTxAUQJEWK%2Fimg.jpg)

> 데이터는 테이블(table)에 Rows로 저장되며,   
> 각 테이블에는 명확하게 정의된 구조(structure)가 있다.  
>   
> 그리고 구조(structure)는 컬럼의 이름과 데이터 유형으로 정의된다.  
>   
> 관계형 데이터베이스에서 스키마를 준수하지 않는 Row는 추가할 수 없다.

※ Records(Rows) : 논리적으로 **연관된 필드의 집합** (**튜플 Tuple**이라고도 함)

※ Fields(Columns) : **가장 작은 단위의 데이터** (엔티티의 속성을 표현)

#### **관계**

또한, 데이터의 중복을 피하기 위해 '**관계**'를 이용한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcQonn8%2FbtrVqheb3Ru%2FW6drPGxytDRRkFTmmGX9x0%2Fimg.jpg)

> 데이터들을 여러 개의 테이블에 나눠서 데이터들의 중복을 피할 수 있다.  
>   
> 테이블을 나눠서 데이터를 저장하면,  
> 테이블에서 중복 없이 하나의 데이터만을 관리하기 때문에   
> 다른 테이블에서 부정확한 데이터를 다룰 위험이 없다.

---

## NoSQL (비관계형 DB)

말 그대로 관계형 DB의 반대다.

**스키마도 없고, 관계도 없다!**

> 💡 여기서 SQL과 핵심적인 차이가 있는데,  
> SQL은 정해진 스키마를 따르지 않으면 데이터 추가가 불가능했다.  
> 하지만 NoSQL에서는 다른 구조의 데이터를 같은 컬렉션에 추가가 가능하다.

대량의 데이터를 빠르게 처리하기 위해 메모리에 임시 저장하고 응답하는 등의 방법을 사용한다. 

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fce6Ufo%2FbtrVsoc68Ei%2FKP7zl092FwxIDQILNdEQC0%2Fimg.png)

NoSQL은 데이터가 테이블에 배치되고

데이터베이스가 생성되기 전에 데이터 구조가 신중하게 설계되는

기존 관계형 데이터베이스의 대안이다.

방대한 분산 데이터 세트로 작업할 때 주로 유용하다.

NoSQL 데이터베이스는 본질적으로 확장 가능하고 고성능이며 유연하다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb5WkUP%2FbtrVpfus4b3%2FpGqHvWnkqI84cDTpJw0cp0%2Fimg.png)

---

### 저장 방식에 따른 NoSQL 데이터베이스 유형

**Key-Value** Model, **Document** Model, **Column** Model, **Graph** Model 4가지 유형으로 분류할 수 있다.

#### 1\. Key-Value Model (키 - 값)

> 가장 기본적인 형태의 NoSQL이며  
> **키 하나로 데이터 하나를 저장하고 조회**할 수 있는 단일 키-값 구조를 갖는다.

> 단순한 저장구조로 인하여 복잡한 조회 연산을 지원하지 않는다.  
>   
> 또한 고속 읽기와 쓰기에 최적화된 경우가 많다.  
> 웹 애플리케이션의 세션 관리 및 캐싱에 매우 적합하다.  
>   
> 하나의 서비스 요청에 다수의 데이터 조회 및 수정 연산이 발생하면,   
> 트랜잭션 처리가 불가능하여 데이터 정합성을 보장할 수 없다.  
> (ex. Redis)  
>   
> ※ 데이터 정합성  
> → 데이터가 서로 모순 없이 일관되게 일치해야 함  
>   
> ※ 트랜잭션  
> → 데이터베이스의 상태를 변환시키는 하나의 논리적 기능을 수행하기 위한 작업의 단위,   
> 또는 한꺼번에 수행되어야할 일련의 연산들을 의미

### 2. Document Model (문서)

> 키-값 모델을 개념적으로 확장한 구조로 **하나의 키에 하나의 구조화된 문서를 저장하고 조회**한다.

> 각 문서에는 주소를 지정하는 고유 키가 있다.  
> 콘텐츠 관리 및 모바일 애플리케이션 데이터 처리에 유용하다.  
>   
> 필드와 값의 형태로 구성된 데이터를 JSON 포맷으로 관리하는 데이터베이스로   
> NoSQL 데이터베이스 중 가장 인기가 높다.  
>   
> 키는 문서에 대한 ID 로 표현된다.  
> 또한 저장된 문서를 컬렉션으로 관리하며 문서 저장과 동시에 문서 ID 에 대한 인덱스를 생성한다.  
> 문서 ID 에 대한 인덱스를 사용하여 O(1) 시간 안에 문서를 조회할 수 있다.  
>   
> 대부분의 문서 모델 NoSQL 은 B 트리 인덱스를 사용하여 2 차 인덱스를 생성한다.  
> B 트리는 크기가 커지면 커질수록 새로운 데이터를 입력하거나 삭제할 때 성능이 떨어지게 된다.  
> 그렇기 때문에 읽기와 쓰기의 비율이 7:3 정도일 때 가장 좋은 성능을 보인다.  
> 중앙 집중식 로그 저장, 타임라인 저장, 통계 정보 저장 등에 사용된다.  
> (ex. MongoDB)

### 3.Column Model (열)

> 칼럼과 로우로 구성된 데이터베이스로  
> **칼럼**은 **이름과 값**으로 구성되고,   
> **로우**는 **각기 다른 칼럼으로 구성**이 가능합니다.

> 하나의 키에 여러 개의 컬럼 이름과 컬럼 값의 쌍으로 이루어진 데이터를 저장하고 조회한다.  
> 모든 컬럼은 항상 타임 스탬프 값과 함께 저장된다.  
>   
> 대부분의 컬럼 모델 NoSQL 은 쓰기와 읽기 중에 쓰기에 더 특화되어 있다.   
> 데이터를 먼저 커밋로그와 메모리에 저장한 후 응답하기 때문에 빠른 응답속도를 제공한다.  
> 그렇기 때문에 읽기 연산 대비 쓰기 연산이 많은 서비스나  
> **빠른 시간 안에 대량의 데이터를 입력하고 조회하는 서비스를 구현**할 때 가장 좋은 성능을 보인다.   
> 채팅 내용 저장, 실시간 분석을 위한 데이터 저장소 등의 서비스 구현에 적합하다.  
>   
> 저장의 기본 단위는 컬럼으로 컬럼은 컬럼 이름과 컬럼 값, 타임스탬프로 구성된다.  
> 이러한 컬럼들의 집합이 로우(Row)이며,  
> 로우키(Row key)는 각 로우를 유일하게 식별하는 값이다.  
> 이러한 로우들의 집합은 키 스페이스(Key Space)가 된다.

### 4\. Graph Model (그래프 데이터베이스)

> 노드(레코드)와 관계로 구성된 데이터베이스로 근접한 객체를 모델링할 목적으로 설계되었다.

> 이 모델은 데이터 관계보다 풍부한 표현을 지원한다.  
> 고객 관계 관리 시스템, 로드맵, 예약 시스템 등에 유용하다.

---

여러 테이블에 조인할 필요없이 이미 필요한 모든 것을 갖춘 문서를 작성하는 것이 NoSQL이다.

(NoSQL에는 조인이라는 개념이 존재하지 않음)

💡 그러면 조인하고 싶을 때 NoSQL은 어떻게 할까?

→ 컬렉션을 통해 데이터를 복제하여

각 컬렉션 일부분에 속하는 데이터를 정확하게 산출하도록 한다.

하지만 이러면 데이터가 중복되어 서로 영향을 줄 위험이 있다.

따라서 조인을 잘 사용하지 않고 자주 변경되지 않는 데이터일 때 NoSQL을 쓰면 상당히 효율적이다.

---

### NoSQL DB 특징

NoSQL 데이터베이스는 각 DBMS별로 차이가 있으나 일반적으로 다음과 같은 특징을 가지고 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FPu4NV%2FbtrVt4e1vys%2FZ6Zk9lGkUukyFNPaKPPWNK%2Fimg.png)

-   유연성 : 스키마 선언 없이 필드의 추가 및 삭제가 자유로운 Schema-less 구조이다.
-   확장성 : 스케일 아웃에 의한 서버 확장이 용이하다.
-   고성능 : 대용량 데이터를 처리하는 성능이 뛰어나다.
-   가용성 : 여러 대의 백업 서버 구성이 가능하여 장애 발생 시에도 무중단 서비스가 가능하다.

---

## 수직적,  수평적 확장(Scaling)

두 부류의 데이터베이스를 살펴볼 때 확장(Scaling)에 대한 개념을 살펴봐야 한다.

각각의 데이터베이스는 어떤 방식으로 확장시킬 수 있을까?

확장은 수직적 확장과 수평적 확장으로 구별할 수 있다.

-   수직적 확장 : 단순히 데이터베이스 서버의 성능을 향상시키는 것 (ex. CPU 업그레이드)
-   수평적 확장 : 더 많은 서버가 추가되고 데이터베이스가 전체적으로 분산됨을 의미 (하나의 데이터베이스에서 작동하지만 여러 호스트에서 작동)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FsDHgm%2FbtrVpYUtHea%2FOkHAMZTeIWxthlIASesQ0K%2Fimg.jpg)

데이터 저장 방식으로 인해 SQL 데이터베이스(관계형)는 일반적으로 수직적 확장만 지원한다.

수평적 확장은 NoSQL 데이터베이스에서만 가능하다.

---

## 어떤 것을 택할까?

정답은 없다. 둘다 훌륭한 솔루션이고 어떤 데이터를 다루느냐에 따라 선택을 고려해야한다.

|   | SQL | NoSQL |
| --- | --- | --- |
| 장점 | ● 명확하게 정의된 스키마, 데이터 무결성 보장      ● 관계는 각 데이터를 중복없이 한 번만 저장 | ● 스키마가 없어서 유연함. 언제든지 저장된 데이터를 조정하고 새로운 필드 추가 가능      ● 데이터는 애플리케이션이 필요로 하는 형식으로 저장됨. 데이터 읽어오는 속도 빨라짐      ●  수직 및 수평 확장이 가능해서 애플리케이션이 발생시키는 모든 읽기/쓰기 요청 처리 가능 |
| 단점 | ● 덜 유연함. 데이터 스키마를 사전에 계획하고 알려야 함.   (나중에 수정하기 힘듦)      ● 관계를 맺고 있어서 join문이 많은 복잡한 쿼리가 만들어질 수 있음      ● 대체로 수직적 확장만 가능함 | ● 유연성으로 인해 데이터 구조 결정을 미루게 될 수 있음      ● 데이터 중보글 계속 업데이트 해야 함      ● 데이터가 여러 컬렉션에 중복되어 있기 떄문에 수정 시 모등 컬렉션에서 수행해야 함   (SQL에서는 중복 데이터가 없으므로 한 번만 수행이 가능) |
| 사용이 더 좋을 때 | ● 관계를 맺고 있는 데이터가 자주 변경되는 애플리케이션의 경우   (NoSQL에서는 여러 컬렉션을 수정해야 하기 때문에 비효율적)      ● 변경될 여지가 없고, 명확한 스키마가 사용자와 데이터에게 중요한 경우 | ● 정확한 데이터 구조를 알 수 없거나 변경 / 확장 될 수 있는 경우      ● 읽기를 자주 하지만, 데이터 변경은 자주 없는 경우      ● 데이터베이스를 수평으로 확장해야 하는 경우(막대한 양의 데이터를 다뤄야 하는 경우) |

하나의 제시 방법이지 완전한 정답이 정해져 있는 것은 아니다.

SQL을 선택해서 복잡한 JOIN문을 만들지 않도록 설계하여 단점을 없앨 수도 있고, 

NoSQL을 선택해서 중복 데이터를 줄이는 방법으로 설계해서 단점을 없앨 수도 있다.

---

### 출처

-   [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/SQL%EA%B3%BC%20NOSQL%EC%9D%98%20%EC%B0%A8%EC%9D%B4.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/SQL%EA%B3%BC%20NOSQL%EC%9D%98%20%EC%B0%A8%EC%9D%B4.md)
-   [https://github.com/JaeYeopHan/Interview\_Question\_for\_Beginner/tree/master/Database#nosql](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Database#nosql)
-   [https://www.integrate.io/ko/blog/sql-vs-nosql-5-critical-differences-ko/](https://www.integrate.io/ko/blog/sql-vs-nosql-5-critical-differences-ko/)
-   [https://ko.myservername.com/sql-vs-nosql-exact-differences](https://ko.myservername.com/sql-vs-nosql-exact-differences)
-   [https://overcome-the-limits.tistory.com/283](https://overcome-the-limits.tistory.com/283)
-   [https://93jpark.tistory.com/23](https://93jpark.tistory.com/23)
-   [https://meetup.nhncloud.com/posts/274](https://meetup.nhncloud.com/posts/274)