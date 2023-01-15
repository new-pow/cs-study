들어가기 전...

## 인덱스(Index)란 무엇인가?

> DBMS도 데이터베이스 테이블의 모든 데이터를 검색해서  
> 원하는 결과를 가져오려면 시간이 오래 걸린다.  
>   
> 그래서 칼럼의 값과 해당 레코드가 저장된 주소를  
> 키와 값의 쌍으로 인덱스를 만들어 두는 것이다.  
>   
> DBMS의 인덱스는 항상 정렬된 상태를 유지하기 때문에   
> 원하는 값을 탐색하는데는 빠르지만   
> 새로운 값을 추가하거나 삭제, 수정하는 경우에는 쿼리문 실행 속도가 느려진다. (뒤에 나옴)  
> → 결론적으로 DBMS 에서 인덱스는  
> 데이터의 저장 성능을 희생하고 그 대신 **데이터의 읽기 속도를 높이**는 기능이다.

그래서 

## 인덱스의 목적

> 추가적인 쓰기 작업과 저장 공간을 활용하여   
> 데이터베이스 테이블의 검색 속도를 향상시키기 위한 자료구조.  
>   
> 즉, **데이터베이스의 테이블에 대한 검색 속도를 향상시켜주는 자료구조**이다. 

> ※ 만약 우리가 책에서 원하는 내용을 찾는다고 하면,   
> 책의 모든 페이지를 찾아 보는 것은 오랜 시간이 걸린다.  
>   
> 그렇기 때문에 책의 저자들은 책의 맨앞 또는 맨뒤에 색인을 추가하는데,,   
> 데이터베이스의 index는 책의 색인과 같다.  
>   
> 즉, 데이터베이스에서도 테이블의 모든 데이터를 검색하면 시간이 오래 걸리기 때문에   
> 데이터와 데이터의 위치를 포함한 자료구조를 생성하여 빠르게 조회할 수 있도록 돕는다.

테이블의 특정 컬럼(Column)에 인덱스를 생성하면, 

해당 컬럼의 데이터를 정렬한 후 별도의 메모리 공간에 데이터의 물리적 주소와 함께 저장된다. 

컬럼의 값과 물리적 주소를 (key, value)의 한 쌍으로 저장한다. 

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmVaOU%2FbtrVLwcBoDk%2FJimbbio6rV7Xh3UxAkASJ1%2Fimg.png)

---

## 인덱스(Index)의 장단점

### <장점>

> **테이블을 검색하는 속도와 성능이 향상**된다.  
> 또 그에 따라 **시스템의 전반적인 부하를 줄일 수 있다**.

> 💡 핵심은 인덱스에 의해 **데이터들이 정렬된 형태를 갖는다는 것**이다.  
> 이 특징으로 인해 조건 검색 시 굉장한 장점이 된다.  
>   
> 예를 들어,   
> 기존엔 WHERE문으로 특정 조건의 데이터를 찾기 위해   
> 테이블 전체를 조건과 비교해야 하는 '풀 테이블 스캔(Full Table Scan)' 작업이 필요했는데,   
> 인덱스를 이용하면 데이터들이 정렬되어 있어 조건에 맞는 데이터를 빠르게 찾을 수 있다.  
>   
> 또 ORDER BY 문이나 MIN/MAX 같은 경우도   
> 이미 정렬이 되어 있기 때문에 빠르게 수행할 수 있다.

### <단점>

> 인덱스의 가장 큰 문제점은   
> **정렬된 상태를 계속 유지시켜줘야 한다**는 점이다.

> 따라서 인덱스가 적용된 컬럼에 삽입(INSERT), 삭제(DELETE), 수정(UPDATE) 작업을 수행하면  
> 다음과 같은 추가 작업이 필요하다.   
>   
> **\- INSERT : 새로운 데이터에 대한 인덱스를 추가**  
> **\- DELETE : 삭제하는 데이터의 인덱스를 사용하지 않는다는 작업 수행**  
> **\- UPDATE : 기존의 인덱스를 사용하지 않음 처리, 갱신된 데이터에 대한 인덱스 추가**  
>   
> 즉, 데이터 변경 작업이 자주 일어나는 경우, **Index를 재작성**해야 하므로 성능에 영향을 미친다.  
>   
> 이처럼 인덱스의 수정도 추가적으로 필요하기 때문에 데이터의 수정이 잦은 경우 성능이 낮아진다.

또한 

-   인덱스를 관리하기 위해 DB의 약 10%에 해당하는 저장공간이 필요하다.
-   인덱스를 관리하기 위해 추가 작업이 필요하다.
-   인덱스를 잘못 사용할 경우 오히려 성능이 저하되는 역효과가 발생할 수 있다.

> 앞에서 UPDATE와 DELETE는  
> 기존의 인덱스를 삭제하지 않고 '사용하지 않음' 처리를 해준다고 하였다.  
>   
> 만약 어떤 테이블에 UPDATE와 DELETE가 빈번하게 발생된다면  
> 실제 데이터는 10만건이지만 인덱스는 100만 건이 넘어가게 되어,  
> SQL문 처리 시 비대해진 인덱스에 의해 오히려 성능이 떨어지게 될 것이다. 

---

## 인덱스(index)를 사용하면 좋은 경우

-   규모가 작지 않은 테이블
-   INSERT, UPDATE, DELETE가 자주 발생하지 않는 컬럼
-   JOIN이나 WHERE 또는 ORDER BY에 자주 사용되는 컬럼
-   데이터의 중복도가 낮은 컬럼

인덱스를 사용하는 것 만큼이나 생성된 인덱스를 관리해주는 것도 중요하다.

그러므로 사용되지 않는 인덱스는 바로 제거를 해주어야 한다. 

---

## 인덱스의 자료구조

> 인덱스는 여러 자료구조를 이용해서 구현할 수 있는데, 대표적으로 해시 테이블(Hash Table)과 B+Tree가 있다. 

### 1\. 해시 테이블 (Hash Table)

> 해시 테이블은 (Key, Value)를 한 쌍으로 데이터를 저장하는 자료구조로   
> **빠른 데이터 검색이 필요할 때 유용**하다.  
>   
> 해시 테이블은 Key값을 이용해 고유한 index를 생성하여 그 index에 저장된 값을 꺼내오는 구조이다.

※ 해시 테이블의 시간복잡도는 O(1)이며 매우 빠른 검색을 지원한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FzX9Yr%2FbtrVOTrdpXD%2FPjPMLm1whtLW7v8r9sopc0%2Fimg.png)

> 해시 테이블을 이용한다면 인덱스는 (key, value) = (컬럼의 값, 데이터의 위치)로 구현하는데,  
> 해시 테이블은 실제로 인덱스에서 잘 사용되지 않는다.   
>   
> 그 이유는, **해시 테이블은 등호(=) 연산만에 최적화되어있기 때문**이다.  
>   
> 해시 함수는 값이 1이라도 달라지면 완전히 다른 해시 값을 생성하는데,  
> 이러한 특성에 의해   
> 부등호 연산(>, <)이 자주 사용되는 데이터베이스 검색을 위해서는 해시 테이블이 적합하지 않다.  
>   
> 이러한 이유로 데이터베이스의 인덱스에서는 B+Tree가 일반적으로 사용된다.

### 2\. B+Tree

> B+Tree는 DB의 인덱스를 위해 자식 노드가 2개 이상인 B-Tree를 개선시킨 자료구조이다.

RDB에서 인덱스는 일반적으로 B+트리 자료구조를 이용하여 검색을 수행하며,

B+ 트리는 다음과 같이 구성된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FpaOYl%2FbtrVStyj6pR%2FPt5EhAM628aTKIrKKuYXb1%2Fimg.png)

-   실제 데이터가 저장된 **리프노드**( Leaf nodes )
-   리프노드까지의 경로 역할을 하는 **논리프노드**( Non-leaf nodes )
-   경로의 출발점이 되는 **루트 노드**( Root node )

> B+Tree는 오직 leaf node에만 데이터를 저장하고  
> leaf node가 아닌 node에서는 자식 포인터만 저장한다.  
>   
> 즉, B+트리의 검색은 루트노드에서 어떤 리프 노드에 이르는 한 개의 경로만 검색하면 되므로, 매우 효율적이다.

※ 더 자세한 정보 : [https://rebro.kr/167](https://rebro.kr/167)

## 정리

-   해시 테이블
    -   컬럼의 값으로 생성된 해시를 기반으로 인덱스를 구현한다.
    -   시간복잡도가 O(1)이라 검색이 매우 빠르다.
    -   부등호(<,>)와 같은 연속적인 데이터를 위한 순차 검색이 불가능하기 때문에 사용에 적합하지 않다.

-   B+Tree 인덱스 자료구조
    -   자식 노드가 2개 이상인 B-Tree를 개선시킨 자료구조이며,
    -   BTree 리프노드들을 LinkedList로 연결하여 순차 검색을 용이하게 한다. 해시 테이블보다 나쁜 O(log2N)의 시간복잡도를 갖지만 일반적으로 사용되는 자료구조이다.

---

### 출처

-   [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/%5BDB%5D%20Index.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/%5BDB%5D%20Index.md)
-   [https://github.com/JaeYeopHan/Interview\_Question\_for\_Beginner/tree/master/Database#index](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Database#index)
-   [https://rebro.kr/167](https://rebro.kr/167)
-   [https://mangkyu.tistory.com/96](https://mangkyu.tistory.com/96)
-   [https://coding-factory.tistory.com/746](https://coding-factory.tistory.com/746)
-   [https://victorydntmd.tistory.com/319](https://victorydntmd.tistory.com/319)
-   [https://dev-coco.tistory.com/158](https://dev-coco.tistory.com/158)