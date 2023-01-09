# JOIN

`SELECT` 문은 하나 이상의 테이블로부터 데이터를 가져온다.

```sql
SELECT info FROM table1, table2
```

테이블 `JOIN` 은 복수의 테이블들이 **서로 연관 맺고 이들로부터 원하는 특정 조건의 데이터셋을 선별**하여 하나의 결과 집합으로 추출한다.

테이블 조인에는 다음과 같은 종류들이 있다.

- Inner Join
- Outer Join
- Cross Join
- Self Join

# INNER JOIN

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F99685eb6-e7d6-4956-bced-e5674b128035%2FUntitled.png?id=c894d5fc-3643-4284-b69a-45f04fc41cc5&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

- 복수 테이블들이 조인 조건을 모두 만족하는 데이터만 가져온다.
- **두 테이블에 모두 조건에 해당하는 데이터가 있어야 한다.**
- 표현 방법은 두 가지가 있다.
    1. `INNER JOIN` ~ `ON` ~ 문장을 `FROM` 절에 사용
    2. 일반 `WHERE` 절에서 조인 조건식 사용

```sql
SELECT a.empno
     , a.ename
     , a.job
     , a.mgr
     , a.deptno
     , b.dname
  FROM emp AS a
 INNER JOIN dept AS b
    ON a.deptno = b.deptno
```

```sql
SELECT * FROM Reservation, Customer
WHERE Reservation.Name = Customer.Name;
```

# OUTER JOIN

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fc872b2dc-cd65-432e-91a6-cdab7898278d%2FUntitled.png?id=1c52eb20-9ce3-4eec-a2b2-244f984172a5&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

- 한쪽에만 데이터가 있어도 결과가 나온다.

```sql
SELECT <열 목록>
FROM <첫 번째 테이블(LEFT 테이블)>
    <LEFT | RIGHT | FULL> OUTER JOIN <두 번째 테이블(RIGHT 테이블)>
	   ON <조인될 조건>
[WHERE 검색 조건]
```

- 만약 ‘짱구’, ‘철수’, ‘흰둥이’의 달리기 기록을 기준으로 찾을 때. ‘흰둥이’의 달리기 기록이 없다면?
    - Inner Join : 짱구, 철수의 기록만 나옴
    - Outer Join : 모두의 기록이 나옴.
- 사용 예제

```sql
SELECT c.Name, SUM(s.Total) '합계'
FROM City c **LEFT OUTER JOIN** Sales s
ON c.Code = s.CityCode
GROUP BY c.Name
```

- 종류
    - FULL OUTER JOIN
    - LEFT OUTER JOIN
    - RIGHT OUTER JOIN

## LEFT JOIN

- 첫 번째 테이블을 기준으로 두 번째 테이블을 조합하는 JOIN
- 데이터가 `ON` 절의 조건을 만족하지 않은 경우에
    - 첫 번째 테이블의 필드값은 그대로 가져온다.
    - 두 번째 테이블의 필드값은 모두 `NULL`로 표현된다.

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID=Orders.CustomerID
ORDER BY Customers.CustomerName;
```

- [예제 링크](https://www.w3schools.com/sql/trysql.asp?filename=trysql_select_join_left)

## RIGHT JOIN

- 두 번째 테이블을 기준으로, 첫 번째 테이블을 조합한다.
- `LEFT JOIN` 과는 반대이나 똑같이 기능한다.

```sql
SELECT Orders.OrderID, Employees.LastName, Employees.FirstName
FROM Orders
RIGHT JOIN Employees
ON Orders.EmployeeID = Employees.EmployeeID
ORDER BY Orders.OrderID;
```

- [예제 링크](https://www.w3schools.com/sql/trysql.asp?filename=trysql_select_join_right&ss=-1)

## FULL OUTER JOIN

- 조건에 맞는 첫번째 테이블, 두번째 테이블의 모든 레코드들을 조합한다.

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
FULL OUTER JOIN Orders
ON Customers.CustomerID=Orders.CustomerID
ORDER BY Customers.CustomerName;
```

# CROSS JOIN

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ff136ef16-08c2-4f52-bba0-0b49f1010091%2FUntitled.png?id=1f8ca8b9-c250-4dcb-b6b2-55f3ad5d22b3&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

- 한쪽 테이블의 모든 행과 다른 쪽 테이블의 모든 행을 조인시킨다.
- 카티션 곱(Cartesial Product)라고도 한다.

```sql
SELECT * 
FROM table1 
CROSS JOIN table2;
```

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fec866cf4-8d64-4cc1-9b6c-19153e2d858d%2FUntitled.png?id=25abfe58-7ddc-4b14-86ec-65f3808d819a&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

- 테이블간의 **관계를 나타내지 않고 조인하는 방법**
    - 1번 쿼리문과 2번 쿼리문의 결과는 같다.

```sql
// 1번
SELECT * FROM Meals 
CROSS JOIN Drinks
```

```sql
// 2번
SELECT * FROM Meals,Drinks
```

# SELF JOIN

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F37325704-d14d-4774-92a9-2b2743701313%2FUntitled.png?id=25ac0928-15dd-4de6-92f6-432a4f712451&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

- 보통의 JOIN 과 똑같이 기능한다.
- 그러나 자신의 테이블과 조인한다.
    - 원본 테이블이 있고, 그 원본 테이블의 복사본을 생성하는 것.
- 문법은 다른 조인과 다를바 없다.

```sql
SELECT
 cust.customer_id,
 cust.firstname,
 cust.lastname,
 cust.birthdate,
 cust.spouse_id,
 spouse.firstname AS spouse_firstname,
 spouse.lastname AS spouse_lastname
FROM **customer AS cust**
INNER JOIN **customer AS spouse**
   ON cust.spouse_id = spouse_id;
```

- [예제 링크](https://www.w3schools.com/sql/trysql.asp?filename=trysql_select_join_self)

## 👀 왜 SELF JOIN 이 필요할까?

셀프 조인은 주로 이런 상황에서 사용한다.

1. 위계성 데이터를 다룰 때
2. 순차성 데이터를 다룰 때
3. 1개의 테이블 안에 관계성이 명시되어야 할 데이터가 여러개 존재할 때

### 위계성 데이터의 사례

- 직속 상관의 이름이 필요함

```sql
SELECT
 e.id,
 e.first_name,
 e.last_name,
 e.salary,
 m.first_name AS boss_first_name
 m.last_name AS boss_last_name
FROM employee AS e
INNER JOIN employee AS m
      ON e.manager_id = m.id;
```

- 이 외에도 가족 족보와 같은 상황 등

### 순차성 데이터의 사례

food

- 순서를 재정의할 때.

```sql
SELECT a.id, a.content
FROM food AS a
INNER JOIN food AS b
WHERE a.id = b.next_id
```

### ****1개의 테이블 안에 관계성이 명시되어야 할 데이터가 여러개 존재할 때****

- 비행기 항로, 기차 여정 등
- 중복 값을 찾아낼 때

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F4e1c86b5-0fad-4e80-ba7a-3dc860d99a24%2FUntitled.png?id=5fe3e1f0-33bb-481d-8c40-7446f9ebd746&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

```sql
SELECT
 start.name AS start_city,
 destination.name AS destination_city
FROM **city** AS start
INNER JOIN route AS r
      ON start.id = r.from_city_id
INNER JOIN **city** AS destination
     ON destination.id = r.to_city_id;
```

- 위 예시는 결국 B테이블을 통해 A와 A 테이블을 연결해준다. 그렇기 때문에 이를 셀프조인이라고 할 수 있다.

---

```sql
SELECT
 c1.id AS id1,
 c1.name AS color1,
 c2.id As id2,
 c2.name AS color2
FROM color AS c1
INNER JOIN color AS c2
      ON c1.name = c2.name
   AND c1.id < c2.id; // 동일한 데이터를 중복으로 인식하지 않기 위해.
```

---

- 참고
    - [혼공이들의 스터디 공간](https://hongong.hanbit.co.kr/sql-%EA%B8%B0%EB%B3%B8-%EB%AC%B8%EB%B2%95-joininner-outer-cross-self-join/)
    - [TCPschool](http://www.tcpschool.com/mysql/mysql_multipleTable_join)
    - [SELF JOIN (上) : 같은 테이블을 조인하기](https://kimsyoung.tistory.com/entry/SELF-JOIN-%E4%B8%8A-%EA%B0%99%EC%9D%80-%ED%85%8C%EC%9D%B4%EB%B8%94%EC%9D%84-%EC%A1%B0%EC%9D%B8%ED%95%98%EA%B8%B0)