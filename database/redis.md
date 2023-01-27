## 들어가기 전...

30년이 넘는 시간동안 RDBMS(Relational DataBase Management System)가 사랑받고 있지만,

대용량 데이터 저장, 비정형 데이터 저장, 빠른 응답시간 등의 새로운 요구사항에

기존 RDBMS만으론 대응하기 어려울 때가 있다.

그럴 때 기존 RDBMS와 차별적인 강점을 갖춘 데이터베이스 관리 프로그램들, NoSql을 찾게 된다.

> ※ NoSql?  
> NoSql은 기존 RDBMS 방식을 탈피한 데이터베이스를 의미한다.

> ※ NoSql의 종류 (NoSql은 RDBMS가 아님)  
> \- 서로 연관된 그래프 형식의 데이터를 저장할 수 있는 Graph Store  
> \- Row가 아닌 Column 위주로 데이터를 저장하는 Column Store  
> \- 비정형 대량 데이터를 저장하기 위한 Document Store  
> \- 메모리 기반으로 빠르게 데이터를 읽어올 수 있는 Key-Value Store

이 중 레디스는 세계에서 가장 인기있는 Key-Value Store 중 하나이다.

## 레디스(Redis)란?

> 빠른 오픈 소스 인 메모리 키 값 데이터 구조 스토어.  
>   
> Remote Dictionary Server의 약자로,  
> **원격 Dictinary 자료구조 서버**라는 직관적인 이름을 가지고 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbc8NKa%2FbtrWRD2NmlC%2F8crJY06kBcJkZJUdXCKKb1%2Fimg.png)

Key로 올 수 있는 자료형은 기본적으로 String이지만, 

Value는 다양한 타입을 지원한다.

데이터 구조는 key/value 값으로 이루어져 있다.

(따라서 Redis는 비정형 데이터를 저장하는 비관계형 데이터베이스 관리 시스템이다.)

---

## 레디스의 데이터 구조 (Value 5가지)

#### 1\. String (text, binary data)

> 거의 대부분의 데이터를 문자열로 표현한다.   
>   
> 예를 들어, 숫자나 날짜 및 시간 등을 문자열로 저장한다고 생각하면 된다.  
>   
> 512MB까지 저장이 가능하다.

#### 2\. 해시 (Hash)

> 해시는 필드를 가질 수 있다.   
>   
> 예를 들어, 사용자 정보라는 해시가 있다면   
> 이메일과 닉네임을 가질 수 있다.   
>   
> 해시는 전체를 가져오거나 개별 필드를 가져올 수 있다.

#### 3\. 리스트 (List)

> 연결 리스트(Linked List)이다.   
> 배열의 왼쪽, 오른쪽에 엘리먼드를 추가할 수 있다.  
>   
> 리스트 안의 데이터는 문자열만 가능하다.  
>   
> 양방향 연결리스트도 가능하다.

#### 4\. 셋 (Set)

> 셋은 리스트와 유사한 특징을 보이지만,  
> 고유 값(Distinck value)을 지정한다는 점에서 차이점이 있다,  
>   
> 고유 값이 이미 정해진 셋에는 고유 값에 해당하는 멤버를 생성할 수 없다.  
>   
> 또한 셋은 정렬을 할 수 있다. (Sorted Set)  
> 정렬을 통해서 특정 기준 값에 들어온 데이터만 필터링하는 게 가능하다.

#### 5\. Sorted Set

> Set을 정렬해둔 상태이다.

---

### 출처

-   [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/Redis.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/Redis.md)
-   [https://brunch.co.kr/@skykamja24/575](https://brunch.co.kr/@skykamja24/575)
-   [https://sihyung92.oopy.io/database/redis/1](https://sihyung92.oopy.io/database/redis/1)