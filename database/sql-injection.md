## SQL Injection이란?

> 악의적인 사용자가 보안상의 취약점을 이용하여,   
> 임의의 SQL 문을 주입하고 실행되게 하여  
> 데이터베이스가 비정상적인 동작을 하도록 조작하는 행위

※ 인젝션 공격은 OWASP Top10 중 첫 번째에 속해 있으며, 

공격이 비교적 쉬운 편이고 공격에 성공할 경우 큰 피해를 입힐 수 있는 공격

(OWASP이란?

→ 보안 취약점 등을 연구하고, 10대 웹 애플리케이션의 취약점(OWASP TOP 10)을 발표)

---

## 왜 발생할까?

> 웹 어플리케이션은 User의 행동(클릭, 입력 등)에 따라   
> DB에 있는 데이터를 서로 다르게 표시한다.  
>   
> 이를 위해 Query는 User가 입력한 데이터를 포함하여 Dynamic하게 변하므로   
> 개발자가 의도하지 않은 정보를 열람할 수 있게 된다.

---

## 주로 어떨 때 발생할까?

> 클라이언트의 입력값을 조작하여  
> 서버의 데이터베이스를 공격할 수 있는 공격 방식이다.  
>   
> 주로 사용자가 입력한 데이터를 제대로 필터링, 이스케이핑(어떤 것을 문자 하나로 인식)하지 못했을 경우에 발생한다.  
>   
> 공격의 쉬운 난이도에 비해 파괴력이 어마어마하다.

※ 유머

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbNSfSH%2FbtrVkXuHGk4%2FrHhJ4pPukx1q3VFCXjBdw0%2Fimg.jpg)

→ 과속방지 카메라에 SQL Injection 하기

---

## 공격 방법

#### 1\. 인증 우회

보통 로그인을 할 때, 아이디와 비밀번호를 input 창에 입력한다.  
  
가벼운 예를 들어보자.

아이디가 abc, 비밀번호가 만약 1234일 때 쿼리는 아래와 같은 방식으로 전송될 것이다.

```sql
SELECT * FROM USER WHERE ID = "abc" AND PASSWORD = "1234";
```

🚨 SQL Injection을 시도하려는 공격자가

비밀번호를 ' OR '1' = '1라고 입력하면?

```sql
SELECT * FROM USER WHERE ID = "admin" AND PASSWORD ='' OR '1' = '1';
```

→ 자세히 살펴보자.

따옴표를 올바르게 닫으며 `password=' '`를 만듦과 동시에 SQL 구문 뒤에 

`' OR '1' = '1`'을 붙였다.

WHERE 뒤에 있는 구문을 간단히 축약하면 **false** AND **false** OR **true**로 정리할 수 있는데, 

논리학에 따르면 AND 연산은 OR보다 연산 우선순위가 빠르다.

따라서 해당 구문의 연산 값은 **true**가 되어 올바른 값으로 판단되고, 실행하게 된다.

이렇게 DB를 마음대로 조작할 수 있다.

#### 2\. 데이터 노출

> 시스템에서 발생하는 에러 메시지를 이용해 공격하는 방법이다.

보통 에러는 개발자가 버그를 수정하는 면에서 도움을 받을 수 있는 존재다.

해커들은 이를 역이용해 악의적인 구문을 삽입하여 에러를 유발시킨다.

즉 예를 들면, 

**❗ GET 방식으로 동작하는 URL 쿼리 스트링을 추가하여 에러를 발생**시킨다.

이에 해당하는 오류가 발생하면,

이를 통해 해당 웹앱의 데이터베이스 구조를 유추할 수 있고 해킹에 활용한다.

예를 들면, 

로그인 폼도 결국엔 서버에 요청을 해서 받는 것이다.

HTTP 헤더를 보면 응답 헤더에 서버의 종류와 버전이 나온다.

Apache 서버는 MySQL 서버, IIS는 MS SQL 같은 방식으로 

데이터베이스의 종류를 추측할 수 있다.

#### 3\. UNION 명령어를 이용한 SQL Injection

※ SQL UNION이란?

→ 여러 개의 SQL문을 합쳐 하나의 SQL문으로 만드는 것이다.

예를 들어 

```
select name from classA 
union
select name from classB;
```

를 하게 되면, 

클래스 A와 클래스 B의 이름들이 합쳐져서 출력된다.

🚨 Union 키워드와 함께 컬럼 수를 맞춰서 SELECT 구문을 넣어주게 되면

**두 쿼리문이 합쳐서서 하나의 테이블로 보여지게 된다.**

또 하나의 예를 들면,

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbkeXBY%2FbtrVjQJo1Ai%2FkubM86HNSGqkCKi82suDk0%2Fimg.png)

위의 사진은 Board라는 테이블에서 게시글을 검색하는 쿼리문이다.

입력값(INPUT)을 title과 contents 컬럼의 데이터랑 비교한 뒤 

글자가 있는 게시글을 출력하는 것이다.

여기서 입력값으로 UNION 키워드와 함께 컬럼 수를 맞춰 

SELECT 구문을 넣어주게 되면, 

두 쿼리문이 합쳐져서 하나의 테이블로 보여지게 된다.

**❗** 현재 Injection한 구문은 사용자의 id와 password를 요청하는 쿼리문이 된다.

∴ 인젝션이 성공하면, 사용자의 개인정보가 게시글과 함께 화면에 보여지게 된다.

---

## 방어 방법

#### 1\. input 값을 받을 때, 특수문자 여부 검사하기

(즉, 입력값에 대한 검증이다.)

> 로그인 전, 검증 로직을 추가하여 미리 설정한 특수문자들이 들어왔을 때 요청을 막아낸다.

#### 2\. SQL 서버 오류 발생 시, 해당하는 여러 메시지 감추기

> view를 활용하여 원본 데이터베이스 테이블에는 접근 권한을 높인다.  
> 일반 사용자는 view로만 접근하여 에러를 볼 수 없도록 만든다.

#### 3\. prepared statement 사용하기

> Prepared Statement 구문을 사용하게 되면,   
> 사용자의 입력 값이 데이터베이스의 파라미터로 들어가기 전에   
> DBMS가 미리 컴파일 하여 실행하지 않고 대기한다.

preparestatement를 사용하면, 특수문자를 자동으로 escaping 해준다.  
(statement와는 다르게 쿼리문에서 전달인자 값을 ?로 받는 것)  
이를 활용해 서버 측에서 필터링 과정을 통해서 공격을 방어한다.

※ 참고 : Statement와 Prepared Statement의 특징

[https://iksflow.tistory.com/127](https://iksflow.tistory.com/127)

#### 4\. Error Message 노출 금지

> 데이터베이스 에러 발생 시 따로 처리를 해주지 않았다면,   
> 에러가 발생한 쿼리문과 함께 에러에 관한 내용을 반환해준다.  
>   
> 이때, 테이블명 및 컬럼명 그리고 쿼리문이 노출될 수 있기 때문에   
> 데이터베이스에 대한 오류 발생 시   
> 사용자에게 보여줄 수 있는 페이지를 제작하여야 한다.

---

### 출처

-   [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/SQL%20Injection.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/SQL%20Injection.md)
-   [https://noirstar.tistory.com/264](https://noirstar.tistory.com/264)
-   [https://namu.wiki/w/SQL%20injection](https://namu.wiki/w/SQL%20injection)
-   [https://m.blog.naver.com/lstarrlodyl/221837243294](https://m.blog.naver.com/lstarrlodyl/221837243294)