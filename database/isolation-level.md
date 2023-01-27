## 트랜잭션의 격리수준이란?

> 동시에 여러 트랜잭션이 처리될 때,  
> 트랜잭션끼리 얼마나 서로 고립되어 있는지를 나타내는 것이다.  
>   
> 즉, 간단하게 말해 특정 트랜잭션이 다른 트랜잭션에 변경한 데이터를  
> 볼 수 있도록 허용할지 말지 결정하는 것이다.

## 격리 수준 (4가지)

-   READ UNCOMMITTED (커밋되지 않은 읽기) (레벨 0)
-   READ COMMITTED (커밋된 읽기) (레벨 1)
-   REPEATABLE READ (반복 가능한 읽기) (레벨 2)
-   SERIALIZABLE (직렬화 기능) (레벨 3)

순서대로 **READ UNCOMMITTED의 격리 수준이 가장 낮고,**

**SERIALIZABLE의 격리 수준이 가장 높다.**

즉, 아래로 내려갈수록 트랜잭션 간 격리(고립) 정도가 높아지며,

동시 처리 성능이 떨어지는 것이 일반적이다.

그러나 SERIALIZABLE 격리 수준이 아니라면 크게 성능의 개선이나 저하는 발생하지 않는다.

아래 표는 트랜잭션 격리 수준에 따라 발생하는 문제점이다.

| **격리 수준** | **DIRTY READ** | **NON-REPEATABLE READ** | **PHANTOM READ** |
| --- | --- | --- | --- |
| READ UNCOMMITTED | O | O | O |
| READ COMMITTED |   | O | O |
| REPEATABLE READ |   |   | O(InnoDB는 발생 X) |
| SERIALIZABLE |   |   |   |

위(READ UNCOMMITTED)로 갈수록 격리 수준이 낮아지는데, 

**격리 수준이 낮을수록 더 많은 문제가 발생**한다.

"DIRTY READ"라고도 하는 "READ UNCOMMITTED"는

일반적인 데이터베이스에서는 거의 사용하지 않고,

SERIALIZABLE 역시 동시성이 중요한 데이터베이스에서는 거의 사용되지 않는다.

일반적인 온라인 서비스에서는 READ COMMITTED나 REPEATABLE READ 중 하나를 사용한다.

(Oracle = READ COMMITTED, MySQL = REPEATABLE READ)

---

## READ UNCOMMITTED

> READ UNCOMMITTED 격리 수준에서는   
> **각 트랜잭션의 변경 내용이 COMMIT이나, ROLLBACK 여부와 상관 없이**   
> **다른 트랜잭션에서 보여지게 된다.**

> ※ 예시  
> 사용자1이 A라는 데이터를 B라는 데이터로 변경하는 동안,  
> 사용자2는 아직 완료되지 않은(Uncommitted) 트랜잭션이지만 데이터 B를 읽을 수 있다.  
>   
> 데이터베이스의 일관성을 유지하는 것이 불가능하다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdq7CUw%2FbtrWJV29iKw%2FlNK6oWtFXR0UTueQjGXdaK%2Fimg.png)

→ 위 그림은 다른 트랜잭션이 사용자 B가 실행하는 SELECT 쿼리의 결과에 

어떠한 영향을 미치는지 보여주는 예시이다.

> ※ 그림 설명  
> 1\. 사용자 A는 **emp\_no = 50000, first\_name = 'JuBal'인 새로운 사원을 INSERT** 하고 있다.  
>   
> 2\. 사용자 B는 변경된 내용을 커밋하기도 전에 emp\_no = 50000인 사원을 검색하고 있다.  
>   
> 3\. 하지만 사용자 B는 사용자 A가 INSERT한 사원의 정보를 커밋되지 않은 상태에서도   
> 조회할 수 있다.  
>   
> 4\. 여기서 문제는, 만약 사용자 A가 작업 도중 문제가 발생하여 INSERT된 내용을   
> ROLLBACK 해버린다 하더라도, 사용자 B는 JuBal이 정상적인 사원이라 판단하고   
> 계속해서 처리하게 된다.

> ※ 조금 더 쉬운 예제  
> 1\. A 트랜잭션에서 10번 사원의 나이를 27살에서 28살로 바꿈  
> 2\. 아직 커밋하지 않음  
> 3\. B 트랜잭션에서 10번 사원의 나이를 조회함  
> 4\. 28살이 조회됨 (이를 '더티 리드'라고 한다)  
> 5\. A 트랜잭션에서 문제가 발생해 Rollback함  
> 6\. B 트랜잭션은 10번 사원이 여전히 28살이라고 생각하고 로직을 수행함  
>   
> \- 데이터 정합성에 문제가 많으므로 RDBMS 표준에서는 격리수준으로 인정하지도 않음

이처럼 **어떠한 트랜잭션에서 처리한 작업이 완료되지 않았음(커밋 되지 않음)에도 불구하고,** 

**다른 트랜잭션에서 볼 수 있게 되는 현상을 더티 리드(Dirty Read)**라고 한다.

**더티 리드가 발생되는 격리수준이 READ UNCOMMITTED**이다.

해결 방법 : [https://steady-coding.tistory.com/562](https://steady-coding.tistory.com/562)

---

## READ COMMITTED

> 어떤 트랜잭션의 변경 내용이 COMMIT 되어야만 다른 트랜잭션에서 조회 가능하다.  
>   
> 오라클 DBMS에서 기본으로 사용하고 있고, 온라인 서비스에서 가장 많이 선택됨.

> 이 레벨에서는 위 READ UNCOMMITTED 수준에서 발생할 수 있는  
> **더티 리드(Dirty Read)와 같은 현상은 발생하지 않는다.**  
> 어떠한 트랜잭션에서 데이터를 변경하더라도  
> COMMIT이 완료된 데이터만 다른 트랜잭션에서 조회할 수 있기 때문이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxwbzV%2FbtrWKzFDrkL%2FKBcQegK6BK8FyPkOJlvWK0%2Fimg.png)

> ※ 그림 설명  
> 1.사용자 A는 emp\_no = 50000인 사원의 first\_name을 "JuBal"에서 "Toto"로 수정함  
>   
> 2\. 이때 **새로운 값인 "Toto"는 employees 테이블에 즉시 기록되고,**   
> **이전 값인 "JuBal"은 Undo 영역으로 백업**된다.  
>   
> 3\. 만약 사용자 A가 이러한 변경 내역을 커밋하기 전에   
> 사용자 B가 emp\_no = 50000인 사원을 조회하면,   
> 결과값은 "Toto"가 아닌 이전 값인 "JuBal"이 조회된다.  
>   
> 4\. 여기서 사용자 B의 SELECT 쿼리 결과는 employees의 테이블이 아닌,   
> UNDO 영역의 백업된 레코드에서 가져온 결과이다.  
>   
> 5\. **READ COMMITTED 격리 수준에서는 어떤 트랜잭션에서 변경한 내용이 커밋되기 전까지는**  
> **다른 트랜잭션에서 그러한 변경 내역을 조회할 수 없기 때문**이다.  
>   
> 6\. 최종적으로 사용자 A가 변경된 내용을 커밋하면  
> 그때부터는 다른 트랜잭션에서도 백업된 UNDO영역의 데이터인 "JuBal"이 아닌  
> 새롭게 변경된 "Toto"라는 값을 참조할 수 있다.

> ※ Undo(언두) 로그  
> \- 언두 영역은 UPDATE 문장이나 DELETE와 같은 문장을 데이터를 변경했을 때   
> 변경되기 전의 데이터를 보관하는 곳이다.  
> INSERT 문장의 경우, 해당 데이터의 row id를 저장하고,   
> 이를 이용하여 물리적 메모리에 바로 접근할 수 있도록 보장한다.  
>   
> \- 크게 두 가지 용도로 사용한다.  
> 1\. 트랜잭션의 롤백 대비용  
> 2\. 트랜잭션의 격리 수준을 유지하면서 높은 동시성 제공

## NON-REPEATABLE 발생

> 하나의 트랜잭션 내에서 동일한 SELECT 퀄리를 실행했을 때   
> 항상 같은 겨로가를 보장해야 한다는 REPEATABLE READ 정합성에 어긋나는 것.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FekvEx6%2FbtrWLiXLGDL%2FfUYhLNHKlqkkDrMOyX8Y5K%2Fimg.png)

> ※ 그림 설명  
> 1\. 사용자 B가 BEGIN 명령으로 트랜잭션을 시작하고,  
> first\_name = 'Toto'인 사원을 조회하면 일치하는 데이터가 존재하지 않음  
>   
> 2\. 하지만 이후에 사용자 A가 emp\_no = 50000인 사원의 이름을 'Toto'로   
> 수정하고 커밋한 후 사용자 B는 동일한 SELECT 쿼리로 조회하면   
> 이번에는 결과가 1건이 조회된다.  
>   
> 3\. 별다른 문제는 없어보이나,   
> 사용자 B가 하나의 트랜잭션 내에서 동일한 SELECT 쿼리를 실행했을 때   
> 항상 같은 결과를 보장해야 한다는 "REPEATABLE READ" 정합성에 어긋난다.

---

## REPEATABLE READ

> 트랜잭션이 시작되기 전에 커밋된 내용에 대해서만 조회할 수 있는 격리 수준.  
>   
> MySQL DBMS에서 기본으로 사용되고 있고,   
> 이 격리수준에서는 NON-REPEATABLE READ 부정합이 발생하지 않는다.  
>   
> 하지만 PHANTOM READ 부정합이 발생한다.  
> (InnoDB 스토리지 엔진을 사용할 경우 PHANTOM READ 부정합 발생 X)

> ※ 예시  
> 1\. 10번 트랜잭션이 500000번 사원을 조회  
> 2\. 12번 트랜잭션이 500000번 사원의 이름을 변경하고 커밋  
> 3\. 10번 트랜잭션이 500000번 사원을 다시 조회  
> 4\. 언두 영역에 백업된 데이터 다시 반환  
>   
> 즉, 자신의 트랜잭션 번호보다 낮은 트랜잭션 번호에서 변경된(커밋된) 것만 보게됨.  
> (모든 InnoDB 트랜잭션은 고유한 트랜잭션 번호(순차 증가)를 가지고 있으며,   
> 언두 영역에 백업된 모든 레코드는 변경을 발생시킨 트랜잭션의 번호가 포함되어 있음)

## PHANTOM READ 발생

> 한 트랜잭션 내에서 같은 쿼리를 두 번 실행했는데,   
> 첫 번째 쿼리에서 없던 유령(Phantom) 레코드가 두 번째 쿼리에서 나타나는 현상.  
>   
> REPETABLE READ 이하에서만 발생하고(SERIALIZABLE은 발생하지 않음),  
> INSERT에 대해서만 발생한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fr5Ig3%2FbtrWJc5AyTx%2FizOGC2N7SPsk4s9PRdz9a0%2Fimg.png)

> ※ 그림 설명  
> 1\. 사용자 B는 트랜잭션 BEGIN 후 SELECT 쿼리를 수행한다.  
>   
> 2\. 따라서 이전 REPEATABLE READ 격리 수준에서의 설명처럼  
> 동일한 트랜잭션 내에서는 결과가 동일해야 함.  
>   
> 3\. 하지만 사용자 B가 실행하는 두 번의 SELECT .. FOR UPDATE 쿼리 결과는 서로 다름  
>   
> 4\. 이렇게 **다른 트랜잭션에서 수행한 변경 작업에 의해**  
> **레코드가 보였다가 안보였다가 하는 현상을 PHANTOM READ(PHANTOM ROW)**라고 한다.

---

## SERIALIZABLE

> 가장 단순하고 가장 엄격한 격리수준이다.  
> 또한 동시 처리 성능도 다른 트랜잭션 격리 수준보다 현저히 떨어진다.  
>   
> 트랜잭션이 완료될 때까지 SELECT 문장이 사용(읽기 작업)하는 모든 데이터에  
> Shared Lock(공유 잠금, 읽기 잠금)이 걸린다.  
>   
> 즉, 한 트랜잭션에서 읽고 쓰는 레코드를 다른 트랜잭션에서는 절대 접근 불가함.

---

## 정리

### 트랜잭션 격리 수준

-   **READ** **UNCOMMITTED**: 트랜잭션내에서 커밋하지 않은 데이터에 다른 트랜잭션의 접근이 가능
-   **READ** **COMMITTED**: 트랜잭션내에서 커밋된 데이터만 다른 트랜잭션이 읽는 것을 허용
-   **REPEATABLE** **READ**: 트랜잭션 내에서 한 번 조회한 데이터를 반복해서 조회해도 결과는 동일
-   **SERIALIZABLE**: 가장 엄격한 격리 수준으로 완벽한 읽기 일관성 모드 제공

### 격리 수준에 따라 발생할 수 있는 문제점

-   **DIRTY READ**: 어떠한 트랜잭션에서 처리한 작업이 완료되지 않았음에도 불구하고 다른 트랜잭션에서 볼 수 있게 되는 현상
-   **NON-REPEATABLE READ**: 동일한 SELECT 쿼리를 실행했을 때 항상 같은 결과를 보장해야 한다는 "REPEATABLE READ" 정합성에 어긋나는 현상
-   **PHANTOM READ**: 한 트랜잭션내에서 동일한 쿼리를 두 번 수행했는데, 첫 번째 쿼리에서 존재하지 않던 유령(Phantom) 레코드가 두 번째 쿼리에서 나타나는 현상

---

### 출처

-   [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/Transaction%20Isolation%20Level.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/Transaction%20Isolation%20Level.md)
-   [https://joont92.github.io/db/%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98-%EA%B2%A9%EB%A6%AC-%EC%88%98%EC%A4%80-isolation-level/](https://joont92.github.io/db/%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98-%EA%B2%A9%EB%A6%AC-%EC%88%98%EC%A4%80-isolation-level/)
-   [https://steady-coding.tistory.com/562](https://steady-coding.tistory.com/562)
-   [https://zzang9ha.tistory.com/381](https://zzang9ha.tistory.com/381)