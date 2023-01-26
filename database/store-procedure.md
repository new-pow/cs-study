## 저장 프로시저 (Stroed Procedure)란?

> 실무에서는 프로그램에서 만들어 놓은 SQL문을 저장해 놓고,   
> 필요할 때마다 호출해서 사용하는 방식으로 프로그램을 만든다.  
>   
> 저장 프로시저는 이러한 방식이 가능하도록하는 각 DBMS에서 제공하는 프로그래밍이다.  
>   
> 간단히 말하자면, 여러 쿼리를 하나의 함수로 묶은 것이다.

> 데이터베이스에서 SQL을 통해 작업을 하다보면,  
> 하나의 쿼리문으로 원하는 결과를 얻을 수 없을 때가 생긴다.  
>   
> 원하는 결과물을 얻기 위해 사용할 여러 줄의 쿼리문을  
> 한 번의 요청으로 실행하면 좋지 않을까?  
>   
> 저장 프로시저는 **쿼리문들의 집합**으로,   
> **어떤 동작을 여러 쿼리를 거쳐서 일괄적으로 처리할 때 사용**한다.

![](https://blog.kakaocdn.net/dn/pydKr/btrW0P70tIb/q1YlWAGpyRzyIraLFIvAzK/img.gif)

→ 프로시저를 만들어두면, 애플리케이션에서 여러 상황에 따라 해당 쿼리문이 필요할 때

인자 값만 전달하여 쉽게 원하는 결과물을 받아낼 수 있다.

---

## 저장 프로시저의 특징

-   일련의 작업 절차를 정리해서 저장한 것
-   여러 SQL문을 묶어서 미리 정의해 두고, 하나의 요청으로 실행할 수 있음
-   자주 사용되는 복잡한 작업들을 간단하게 실행할 수 있음
-   Application에서 직접 모든 작업을 요청하지 않아도 되기 때문에 **부하가 줄어들고 보안이 향상됨**
-   단, 검증되지 않은 저장 프로시저를 실행하는 것은 매우 위험함

---

## 프로지서 생성 및 호출

```sql
CREATE OR REPLACE PROCEDURE 프로시저명(변수명1 IN 데이터타입, 변수명2 OUT 데이터타입) -- 인자 값은 필수 아님
IS
[
변수명1 데이터타입;
변수명2 데이터타입;
..
]
BEGIN
 필요한 기능; -- 인자값 활용 가능
END;

EXEC 프로시저명; -- 호출
```

→ 위 코드의 CREATE 부터 END 까지가 저장 프로시저를 구성하는 코드이고,  
하단 부의 EXECUTE 혹은 CALL 문장으로 해당 프로시저를 실행할 수 있다.

\- ARGUMENT(인자값)

: 프로시저가 실행될 때 입력 받을 값 (프로시저 실행 시 입력해줌)

\- BEGIN

: 저장 프로시저 범위의 시작

\- END

: 저장 프로시저 범위의 끝

#### 예시 1 (IN)

```sql
CREATE OR REPLACE PROCEDURE test( name IN VARCHAR2 ) 
IS
	msg VARCHAR2(5) := '내 이름은';
BEGIN 
	dbms_output.put_line(msg||' '||name); 
END;

EXEC test('규글');
```

결과

```
내 이름은 규글
```

#### 예시 2 (OUT)

```sql
CREATE OR REPLACE PROCEDURE test( name OUT VARCHAR2 ) 
IS
BEGIN 
	name := 'Gyoogle'
END;

DECLARE
out_name VARCHAR2(100);

BEGIN
test(out_name);
dbms_output.put_line('내 이름은 '||out_name);
END;
```

결과

```
내 이름은 Gyoogle
```

---

## 프로시저 장점

#### 1\. 네트워크 부하 감소

> 저장 프로시저를 쓰게 된다면 단 한번의 요청으로 여러 SQL문을 실행할 수 있으므로,   
> 네트워크에 대한 부하를 줄일 수 있다.  
> (보통 쿼리는 네트워크를 타고 DB에 전달)

#### 2\. 처리 시간 감소

> 미리 구문 분석 및 내부 중간 코드로 변환을 끝내야 하므로 처리 시간이 줄어들게 된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxKJy2%2FbtrWZXdY3Ik%2FPKSsJVbJWNRLXwaYk1lMnk%2Fimg.png)

> ※ 추가 설명  
> 저장 프로시저는 최조 실행될 때 최적화된 상태로 컴파일이 되고,   
> 이후에 DB에 캐시되어 저장된다.  
>   
> 캐시에 저장되었단 말은, 최적화와 컴파일 작업을 다시 하지 않는다는 이야기이므로  
> 한 저장 프로시저가 여러 번 쓰이면 성능 향상에 도움이 된다.

#### 3\. 데이터 무결성 유지

> 애플리케이션 측에서 특정 작업을 해주지 않아도,   
> 저장 프로시저를 수행하게 되면 DB의 데이터 앞뒤가 맞게 될 수 있다.

#### 4\. 편리한 유지보수 및 개발 업무와의 구분

> 작업이 변경될 때, 다른 작업은 건드리지 않고   
> 프로시저 내부에서 수정만 하면 된다.  
> (But, 장점이 단점이 될 수 있는 부분이기도 하다.)  
>   
> 또한, 저장 프로시저는 DB 서버에 저장되어 API처럼 제공되므로   
> 애플리케이션을 구성하는 소스 코드와 구분될 수 있다.

#### 5\. 절차적 기능 구현 기능

> SQL 문에 IF나 While과 같은 제어문장을 사용할 수 있어서  
> 애플리케이션 소스 코드를 줄일 수 있다.

---

## 프로시저 단점

#### 1\. 불편한 유지보수

> 위의 장점에서 유지보수가 편리하다고 했지만,   
> 프로그램을 개발한 사람과 운영하는 사람이 다르다면 이야기가 달라진다.  
>   
> 아무래도 많은 SQL문이 모여있고,  
> 여러 곳에서 하나의 저장 프로시저를 사용하는 경우가 많을테니  
> 운영을 하기 위해 들어온 인력 입장에서는 한 번에 파악하기도 어렵고  
> 저장 프로시저를 수행하며 발생하는 데이터를 분석하기도 어렵다.

#### 2\. 호환성

> 구문 규칙이 SQL / PSM 표준과의 호환성이 낮기 때문에   
> 코드 자산으로의 재사용성이 나쁘다.

#### 3\. 성능

> 문자 또는 숫자 연산에서 프로그래밍 언어인 C나 Java보다 성능이 느리다.

#### 4\. 디버깅

> 에러가 발생했을 때, 어디서 잘못됐는지 디버깅하는 것이 힘들 수 있다.

++ 최근에는 저장 프로시저를 점점 줄여나가는 추세라고 한다.

---

### 출처

-   [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/%EC%A0%80%EC%9E%A5%20%ED%94%84%EB%A1%9C%EC%8B%9C%EC%A0%80(Stored%20PROCEDURE).md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/%EC%A0%80%EC%9E%A5%20%ED%94%84%EB%A1%9C%EC%8B%9C%EC%A0%80(Stored%20PROCEDURE).md)
-   [https://devkingdom.tistory.com/323](https://devkingdom.tistory.com/323)
-   [https://girrr.tistory.com/124](https://girrr.tistory.com/124)
-   [https://siahn95.tistory.com/entry/DBMSSQL-%EC%A0%80%EC%9E%A5-%ED%94%84%EB%A1%9C%EC%8B%9C%EC%A0%80Stored-Procedure%EB%9E%80](https://siahn95.tistory.com/entry/DBMSSQL-%EC%A0%80%EC%9E%A5-%ED%94%84%EB%A1%9C%EC%8B%9C%EC%A0%80Stored-Procedure%EB%9E%80)