# 트랜잭션 Transaction

### 트랜잭션(Transaction)이란?

> 데이터베이스의 상태를 변화시키기 위해 수행하는 작업 단위

💡 데이터베이스의 상태를 변화시킨다는 것을 무엇일까?

→ SQL 질의어를 통해 DB에 접근하는 것! 

※ SQL 질의어

-   SELECT
-   INSERT
-   DELETE
-   UPDATE

🚨 작업의 단위는 질의어 한문장이 아니다.

작업단위 : 많은 질의어 명령문들을 사람이 정하는 기준에 따라 정하는 것을 의미.

> 예시) 사용자 A가 사용자 B에게 10,000원을 송금한다.  
>   
> ✔️ 이때 DB 작업  
> 1\. 사용자 A의 계좌에서 만원을 차감한다 : UPDATE문을 사용해 사용자 A의 잔고를 변경  
> 2\. 사용자 B의 계좌에서 만원을 추가한다 : UPDATE문을 사용해 사용자 B의 잔고를 변경  
>   
> 💡 현재 작업 단위 : 출금 UPDATE문 + 입금 UPDATE문  
> → 이를 통틀어 하나의 트랜잭션이라고 한다.  
>   
> \- 위 두 쿼리문 모두 성공적으로 완료되어야만  
> "하나의 작업(트랜잭션)"이 **완료**되는 것이다. : commit  
> \- 작업 단위에 속하는 쿼리 중 하나라도 실패하면   
> 모든 쿼리문을 취소하고 **이전 상태로 돌려놓아야** 한다. : Rollback

즉, 하나의 트랜잭션 설계를 잘 만드는 것이 데이터를 다룰 때 많은 이점을 가져다준다.

---

## 트랜잭션의 특징 (ACID)

#### 원자성 (Atomicity)

> 트랜잭션(작업)이 모두 반영되던지, 아니면 전혀 반영되지 않아야 한다.  
> 즉, **All or Nothing**

#### 일관성 (Consistency)

> 트랜잭션의 작업 처리 결과는 항상 일관성이 있어야 한다.

#### 독립성 (Isolation)

> 둘 이상의 트랜잭션이 동시에 병행 실행되고 있을 때,   
> 서로의 연산에 끼어들 수 없다.

#### 지속성 (Durability)

> 트랜잭션이 성공적으로 완료되었으면, 결과는 영구적으로 반영되어야 한다.  
> 즉, 완료된 결과는 영구적으로 반영되어야 한다.

---

## 트랜잭션의 Commit, Rollback 연산

#### Commit

> 하나의 트랜잭션이 성공적으로 끝났고, DB가 일관성있는 상태일 때   
> 이를 알려주기 위해 사용하는 연산.

#### Rollback

> 하나의 트랜잭션 처리가 비정상적으로 종료되어 트랜잭션 원자성이 깨진 경우,   
> 트랜잭션을 처음부터 다시 시작하거나,   
> 트랜잭션의 부분적으로만 연산된 결과를 다시 취소시키앋.

> 💡 즉, 하나의 트랜잭션은 Commit(작업완료)되거나 Rollback(취소)된다.

---

### 트랜잭션의 5가지 상태

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdShbhc%2FbtrV0QVfkcW%2F0oP4tdpAF0swz22rPikDF1%2Fimg.jpg)

-   **활동(Active)** : 트랜잭션이 실행중인 상태
-   **실패(Failed) :** 트랜잭션 실행에 오류가 발생하여 중단된 상태
-   **철회(Aborted) :** 트랜잭션이 비정상적으로 종료되어 Rollback 연산을 수행한 상태
-   **부분 완료(Partially Committed) :** 트랜잭션의 마지막 연산까지 실행했지만, Commit 연산이 실행되기 직전의 상태
-   **완료(Committed) :** 트랜잭션이 성공적으로 종료되어 Commit 연산을 실행한 후의 상태

---

### 출처

-   [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/Transaction.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/Transaction.md)
-   [https://github.com/JaeYeopHan/Interview\_Question\_for\_Beginner/tree/master/Database#transaction](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Database#transaction)
-   [https://dev-coco.tistory.com/158?category=1056309](https://dev-coco.tistory.com/158?category=1056309)
-   [https://mommoo.tistory.com/62](https://mommoo.tistory.com/62)
-   [https://wonit.tistory.com/462](https://wonit.tistory.com/462)
-   [https://coding-factory.tistory.com/226](https://coding-factory.tistory.com/226)

---

<br>
<br>

-   트랜잭션은 하나의 작업 단위를 뜻한다.

```
// 예시

"상품 발송"이라는 트랜잭션의 작업들
1. 포장
2. 영수증 발행
3. 발송
```

-   트랜잭션을 이루는 작업들 중 하나라도 실패하면 3가지 모두 취소하고 “상품 발송” 이전의 상태로 돌려야 한다. == 롤백Rollback
-   트랜잭션은 예외처리와 관련이 깊다.

```java
상품발송() {
    **try {**
        포장();
        영수증발행();
        발송();
    **}catch(예외) {**
        모두취소();  // 하나라도 실패하면 모두 취소
    **}**
}

포장() **throws 예외** {
   ...
}

영수증발행() **throws 예외** {
   ...
}

발송() **throws 예외** {
   ...
}
```

-   만약 메서드에 각각 예외 처리가 되어있다면 어떻게 될까? 생각해보자.

---

-   참고
    -   [점프 투 자바](https://wikidocs.net/229)
- log
	- `22.12.31` Error & Exception 정리하며 관련 내용 정리