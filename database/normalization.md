# 정규화 Normalization

Last edited time: January 16, 2023 9:03 PM
✨ today i learn: https://www.notion.so/2023-01-15-til-5a94c476e9144d12b680e1d1ad506e79, https://www.notion.so/2023-01-16-til-fcc313f0cf5c412b89ed4b256b708900
분류: Database
상태: not to do

January 15, 2023 

---

# DB 정규화 Normalization

- 데이터 중복과 삽입insertion, 수정update, 삭제deletion 변칙을 최소화하기 위해 일련의 normal forms(NF)에 따라 관계형 DB를 구성하는 과정
    - 중복된 데이터는 많은 문제를 일으킨다.
- DB디자인 결과의 평가 이론이 된다.
- 타당한 이유가 있다면, 반드시 가장 높은 정규화까지 만족시킬 필요는 없다.
- 몇가지 원칙만 지키면 정규화가 필요없는 ERD(entity-relationship diagram)를 설계할 수 있다.

## 목적

- 데이터의 중복을 없애면서 불필요한 데이터를 최소화시킨다.
- 무결성Integrity을 지키며 [삽입, 삭제, 갱신 이상 현상](https://itwiki.kr/w/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4_%EC%A0%95%EA%B7%9C%ED%99%94)을 방지한다.
- 테이블 구성을 논리적이고 직관적으로 할 수 있다.
- 데이터베이스 구조 확장에 용이해진다.
- 어떠한 릴레이션이라도 데이터베이스 내에서 표현 가능하게 한다.
- 효과적인 검색 알고리즘 생성이 가능하다.

## NF (normal form)

| Init table | 1NF | 2NF | 3NF | BCNF | 4NF | 5NF | 6NF |
| --- | --- | --- | --- | --- | --- | --- | --- |

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F9fb0f7b1-f6b7-416e-90fe-ee5bbb346bad%2FUntitled.png?id=b8dfe47c-82f1-4fa8-91c8-a8277d39bef5&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

- 초기 테이블부터 순차적으로 진행하며, normal form을 만족하지 못하면 만족하도록 테이블 구조를 조정한다.
- **앞 단계를 만족해야 다음 단계로 진행할 수 있다.**

---

### 1NF ~ BCNF

| 1NF | 2NF | 3NF | BCNF |
| --- | --- | --- | --- |
- `FD`와 `key`만으로 정의되는 normal forms
- `3NF`까지 도달하면 정규화 됐다고 말하기도 한다.

<aside>

#### ❗ `FD`???

- **Functional dependency**
- 어떤 다른 두개의 튜플 `t1`, `t2`와 관계 `r`이 있을때, `t1[X]=t2[X]`을 만족하게 되면 반드시 `t1[Y]=t2[Y]`을 만족해야 하는 제약조건을 뜻한다.
- 관계 스키마가 얼마나 잘 되어있는지를 판단할 수 있는 도구이다.
- relation이 주어지게 되면 어떤 FD인지 찾을 수는 없지만 위반여부를 확인 할 수는 있다.
</aside>

---

## 제 1 정규화 (1NF)

- 모든 속성값들은 원자값(atomic values)이어야 한다.
    - 쉬운 말로 한 칸엔 하나의 데이터만!
- 나중에 찾고 조합하기가 더 쉬워진다.

- **제 1정규형을 만족시키는 테이블**

| 회원번호 | 회원이름 | 수강 프로그램 |
| --- | --- | --- |
| 101 | 강호동 | 수영 초급 |
| 102 | 손흥민 | 헬스 |
| 103 | 김민수 | 헬스 |
| 103 | 김민수 | 수용 초급 |

- **제 1정규형을 만족시키지 못하는 테이블**

| 회원번호 | 회원이름 | 수강 프로그램 |
| --- | --- | --- |
| 101 | 강호동 | 수영 초급 |
| 102 | 손흥민 | 헬스 |
| 103 | 김민수 | 헬스, 수영 초급 |
- 가장 간단한 것은 원자값으로 분해해 튜플로 구분하고 다른 키를 추가하는 것이다.
- 실제로 복잡한 테이블은 이렇게 단순하게 분해해버리면 다른 중복 문제들이 많이 생겨 테이블 구조를 따져봐야한다.

---

## 제 2 정규화

> `Partial dependency`를 제거한 테이블. (부분적 함수 종속을 제거)
> 모든 nonprime attribute가 PK에 의해 full FD로 의존적이어야 한다.

- 완전 함수 종속이 되도록 해야 한다.
- 테이블에서 기본키가 복합키(키1, 키2)로 묶여있을 때, 두 키 중 하나의 키만으로 다른 컬럼을 결정지을 수 있으면 안된다.
- 현재 테이블의 주제와 별로 상관없는 컬럼을 별도로 관리한다.

- 수강 등록 현황 table
    
    
    | 회원번호 | 회원이름 | 수강 프로그램 | 가격 | 납입여부 |
    | --- | --- | --- | --- | --- |
    | 101 | 강호동 | 수영 초급 | 5000 | 0 |
    | 102 | 손흥민 | 헬스 | 6000 | 1 |
    | 103 | 김민수 | 헬스 | 6000 | 1 |
    | 103 | 김민수 | 수용 초급 | 8000 | 0 |
    - 여기서 헬스 가격을 7000원으로 수정하려면? 하나씩 다 찾아가며 수정해야할까??


- **제 2 정규형을 만족시키는 테이블**
    
    
    | 회원번호 | 회원이름 | 수강 프로그램 | 납입여부 |
    | --- | --- | --- | --- |
    | 101 | 강호동 | 수영 초급 | 0 |
    | 102 | 손흥민 | 헬스 | 1 |
    | 103 | 김민수 | 헬스 | 1 |
    | 103 | 김민수 | 수용 초급 | 0 |
    
    | 프로그램 | 가격 |
    | --- | --- |
    | 수영 초급 | 5000 |
    | 헬스 | 7000 |
- 단, 단점으로 다른 테이블의 데이터를 알아야 알 수 있는 정보가 있다.
    - *예시 : 김민수는 총 얼마를 내야하는가?*
- 따라서 비관계형 DB들은 제 2정규화를 안하는 경우도 많다.

<aside>

#### ❗ `Partial dependency` 란 무엇일까?

데이터 베이스에는 데이터 행을 서로 구분하기 위한 `primary key`가 있다. 하지만 매번 1개의 `primary key`가 있는 것은 아니다.

데이터 테이블에 따라 `Composite primary key`로 있을 수 있다.

| 회원번호 | 회원이름 | 수강 프로그램 | 납입여부 |
| --- | --- | --- | --- |
| 101 | 강호동 | 수영 초급 | 0 |
| 102 | 손흥민 | 헬스 | 1 |
| 103 | 김민수 | 헬스 | 1 |
| 103 | 김민수 | 수용 초급 | 0 |

`partial dependency`는 이 중 하나의 Composite primary key의 종속관계에 있는 컬럼을 말한다.

| 회원번호 | 회원이름 | 수강 프로그램 | 가격 | 납입여부 |
| --- | --- | --- | --- | --- |
| 101 | 강호동 | 수영 초급 | 5000 | 0 |
| 102 | 손흥민 | 헬스 | 6000 | 1 |
| 103 | 김민수 | 헬스 | 6000 | 1 |
| 103 | 김민수 | 수용 초급 | 8000 | 0 |
</aside>

---

## 제 3정규화

> 기본키가 아닌 속성들은 기본키에 의존해야 한다.

- 이행적 함수 종속을 제거해야 한다.
    - 이행적 함수 종속: A→B 이고 B→C 일 때 A→C 인 관계
- 테이블의 주제에 상관없고, primary key랑 상관없는 컬럼에 종속된 데이터는 다른 데이터로 분리한다.

| 프로그램 | 가격 | 강사 | 강사 출신대학 |
| --- | --- | --- | --- |
| 스쿼시 | 5000 | 가강사 | 가대 |
| 헬스 | 7000 | 나강사 | 나대 |
| 골프 | 9000 | 다강사 | 다대 |
| 수영 | 5000 | 마강사 | 라대 |
- 제 3정규형을 만족하는 테이블

| 프로그램 | 가격 | 강사 |
| --- | --- | --- |
| 스쿼시 | 5000 | 가강사 |
| 헬스 | 7000 | 나강사 |
| 골프 | 9000 | 다강사 |
| 수영 | 5000 | 마강사 |

| 강사 | 출신대학 |
| --- | --- |
| 가강사 | 가대 |
| 나강사 | 나대 |
| 다강사 | 다대 |
| 마강사 | 라대 |
- 나중에 수정이 편리해진다.
- 단, 단점은 한번에 데이터 정보를 알 수 없다는 것이다. 최소 2개 테이블을 조합해야지 정보를 알 수 있다.

---

## BCNF

> 결정자이면서 후보키가 아닌 것을 제거해야 한다.

| 회원번호 | 수강 프로그램 | 강사 |
| --- | --- | --- |
| 101 | 수영 초급 | 마강사 |
| 102 | 헬스 | 나강사 |
| 103 | 골프 | 다강사 |
| 103 | 수영 초급 | 마강사 |
- 제약사항
    - 각 강사는 하나의 프로그램만 담당
    - 한 프로그램은 여러 강사가 담당 가능
    - 한 학생은 동일한 프로그램에 대해 한 강사에게만 수강 가능
- 회원번호 + 프로그램은 강사를 정해준다.
- 강사는 과목을 정한다.
- 강사도 결정자이지만, 학번을 결정 지울 수 없으므로 후보키는 아니다.
- 수정 후 테이블

| 회원번호 | 프로그램 코드 |
| --- | --- |
| 101 | AAD |
| 102 | AAB |
| 103 | AAC |
| 103 | AAD |

| 프로그램 코드 | 프로그램 | 강사 |
| --- | --- | --- |
| AAA | 스쿼시 | 가강사 |
| AAB | 헬스 | 나강사 |
| AAC | 골프 | 다강사 |
| AAD | 수영 | 마강사 |

![또다른 예시](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F9a6695e4-bdc5-45b6-b7d1-10bca518e48a%2FUntitled.png?id=ab5d5a8a-2443-444b-8738-0e510eb85fa7&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

또다른 예시

## 제 4 정규형

> 다치 종속(Multi-valued Dependency)가 없어야 한다.
> 

<aside>
❗ 다치종속이란?

1. `A→B` 일 때 하나의 A값에 여러 개의 B값이 존재하면 다치 종속성을 가진다고 하고 `A↠B` 라고 표시한다
2. 최소 3개의 칼럼이 존재한다.
3. R(A, B, C)가 있을 때 A와 B 사이에 다치 종속성이 있을 때 B와 C가 독립적이다.
</aside>

![이런 경우 테이블을 분리한다.](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F3f22b01b-27df-46bb-8dfb-c9d362372d15%2FUntitled.png?id=8777978f-3cc8-4957-9cb5-209b989dbc5f&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

이런 경우 테이블을 분리한다.

| 학생번호 | 과목 |
| --- | --- |

| 학생번호 | 취미 |
| --- | --- |

## 제 5 정규형

> 조인 종속 Join dependency 이 없어야 한다.
> 조인 연산을 했을 때 손실이 없어야 한다.

<aside>
❗ 조인 종속??

다치 종속의 좀 더 일반화된 형태이다. 만약 하나의 릴레이션을 여러 개의 릴레이션으로 무손실 분해했다가 다시 결합할 수 있다면 조인 종속이라고 한다.

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F6f544256-698c-41df-81b3-bd062b252815%2FUntitled.png?id=fd39b44b-dec0-4850-8d32-4522f1573813&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

</aside>

- 일반적으로 현실 데이터베이스는 5정규형을 사용하지 않는다.

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fd80f6570-b8a5-47f6-9ba7-c7da62223b1a%2FUntitled.png?id=90581f44-4905-4809-871e-342d589f4486&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

- 개발자와 자격증, 개발자와 언어는 관계가 있으나 자격증과 언어는 관계가 없음
- 관계 엔터티를 각각 독립적 관계로 해소함으로써 이상 현상 해결할 수 있다.

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F7ce5dbd8-32cc-4108-b00c-0cc75b29a5d4%2FUntitled.png?id=4393026b-f4d4-4632-b9fb-174353c14241&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

---

---

- 참고
    - [쉽게 설명하는 데이터 정규화](https://youtu.be/Y1FbowQRcmI)
    - [데이터베이스 정규화](https://itwiki.kr/w/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4_%EC%A0%95%EA%B7%9C%ED%99%94)
    - [5NF](https://www.studytonight.com/dbms/fifth-normal-form.php)
    - [데이터베이스 정규화 개념 설명 및 예제](https://wkdtjsgur100.github.io/database-normalization/)