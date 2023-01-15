좋은 관계형 데이터베이스를 설계하는 목적 중 하나가 

정보의 이상 현상 (Anomaly이 생기지 않도록 고려해 설계하는 것이다.

이상 현상은 테이블을 설계할 때, 

잘못 설계하여 데이터를 삽입, 삭제, 수정할 때 논리적으로 생기는 오류를 말한다.

> 💡 정규화를 해야하는 이유는  
> 잘못된 테이블 설계로 인해 Anomaly(이상 현상)이 나타나기 때문이다.

이상 현상은 

-   갱신 이상 (Update Anomaly)
-   삽입 이상 (Insertion Anomaly)
-   삭제 이상 (Deletion Anomaly)

으로 구성된다.

---

| 학번 | 이름 | 나이 | 성별 | 강의코드 | 강의명 | 전화번호 |
| --- | --- | --- | --- | --- | --- | --- |
| 1011 | 이태호 | 23 | 남 | AC1 | 데이터베이스 개론 | 010-2627-8123 |
| 1012 | 강민정 | 20 | 여 | AC2 | 운영체제 | 010-4665-1941 |
| 1013 | 김현수 | 21 | 남 | AC3 | 자료구조 | 010-5223-4464 |
| 1013 | 김현수 | 21 | 남 | AC4 | 웹 프로그래밍 | 010-5223-4464 |
| 1014 | 이병철 | 26 | 남 | AC5 | 알고리즘 | 010-6305-2912 |

## 1\. 삽입 이상

> 자료를 삽입할 때 의도하지 않는 자료까지 삽입해야만 자료를 테이블에 추가가 가능한 현상.  
> 즉, 불필요한 정보를 함께 저장하지 않고서는 어떤 정보를 저장하는 것이 불가능하다.

※ 표 예시

> 강의를 아직 수강하지 않은 새로운 학생을 삽입할 경우,   
> 강의 코드와 강의명 속성에는 null값이 들어가야 하는 문제가 생긴다.  
>   
> 즉, 불필요한 정보를 함께 입력하지 않는 한 위 테이블에 입력할 수 없다.

## 2\. 갱신 이상

> 중복된 데이터 중 일부만 수정되어 데이터 모순이 일어나는 현상.  
> 즉, 반복된 데이터 중에 일부를 갱신할 시 데이터의 불일치가 발생한다.

※ 표 예시

> 강의 코드가 "AC3"인 김현수의 전화번호를 수정할 경우,   
> 3번째 튜플의 데이터만 수정될 것이다.  
> 그러면 3, 4번째 튜플은 같은 사용자의 데이터임에도 불구하고 전화번호가 다르게 된다.

## 3\. 삭제 이상

> 어떤 정보를 삭제하면, 의도하지 않은 다른 정보까지 삭제되어버리는 현상.  
> 즉, 필요한 정보를 함께 삭제하지 않고서는 어떤 정보를 삭제하는 것이 불가능하다.

※ 표 예시

> 강의코드가 "AC1"인 데이터베이스 개론 강의를 삭제하게 되면,   
> 이태호 학생의 데이터까지 삭제되어버린다.  
>   
> 바꿔말하면,   
> "AC1"의 강의를 듣는 학생은 이태호 학생 단 한명이다.  
> 이태호 학생의 정보(첫 번째 행)를 삭제하면 "AC1" 강의에 대한 정보도 사라지게 된다.

---

이러한 이상 현상을 예방하고 효과적인 연산을 하기 위해

데이터 정규화(Data Normalication)를 한다.

---

### 출처

-   [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/%5BDB%5D%20Anomaly.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/%5BDB%5D%20Anomaly.md)
-   [https://dev-coco.tistory.com/63](https://dev-coco.tistory.com/63)
-   [https://yaboong.github.io/database/2018/03/09/database-anomaly-and-functional-dependency/](https://yaboong.github.io/database/2018/03/09/database-anomaly-and-functional-dependency/)
-   [https://wkdtjsgur100.github.io/anomaly/](https://wkdtjsgur100.github.io/anomaly/)