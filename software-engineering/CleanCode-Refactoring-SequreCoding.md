- [참고 링크1 (출처)](https://github.com/gyoogle/tech-interview-for-developer)
- [참고 링크2 (출처)](https://happygrammer.github.io/guide/clean-code/)

---

## 1. 클린코드(Clean Code)
### 1 - 0. 클린코드란?
> 코드를 작성하는 의도와 목적이 명확하며, 다른 사람이 쉽게 읽을 수 있어야 함.
즉, **가독성**이 좋아야 함.

💡 가독성을 높이려면?
→ 다른 사람이 코드를 봐도 자유롭게 수정이 가능하고, 
버그를 찾고 변경된 내용이 어떻게 상호작용하는지 이해하는 시간을 최소화 시키는 것.
즉, **코드가 잘 읽히는 지, 코드가 지저분하지 않고 정리된 코드인지** 나타낸다.

다음 내용은 '**클린코드를 만들기 위한 규칙**'이다.
### 1 - 1. 네이밍(Naming)
> 변수, 클래스, 메소드에 의도가 분명한 이름을 사용함

* **클래스명** : **명사**를 사용하며 의미가 드러나는 이름을 지음
* **변수** : 의도가 드러나도록 작성함
* **메서드** : 객체의 동작을 의미하므로 **동사**를 사용하여 이름을 지음
* 멤버 변수, 인자명, 로컬 변수명은 lowerCamelCase 방식을 따름
* 상수 변수명은 CONTANT_CASE 방식을 이용함
  ```java
  // Constants
  static final int NUMBER = 5;
  ```
* 범용적으로 사용되는 단어 사용 X (aix, hp 등)
* 연속된 숫자나 불용어를 덧붙이는 방식은 피해야함
```java
// 예
int elapsedTimeInDays;
int daysSinceCreation;
int fileAgeInDays;
```

### 1 - 2. 주석 관리(Comment)
> 불필요한 주석을 제거하고 의도를 명확하게 관리함

#### 1. 중복 주석 제거
> 코드로서 의도를 직관적으로 파악할 수 있다면 주석을 남기지 않아도 됨

#### 2. 정보 제공 주석
> 코드에서 강조할 부분이 있거나, 의도를 직관적으로 파악할 수 없다면 정보 제공 주석을 남겨야 함

```java
private void quicksort(int low, int high) {
        int i = low, j = high;
        // 리스트 중간의 피봇 엘리먼트의 위치
        int pivot = numbers[(low + high) / 2];
        // 하나의 리스트를 두개의 리스트로 나눔
        while (i <= j) {
        ..
}
```

#### 3. 할일 주석
> 차기 기능 요소 추가시 유용하게 사용 가능함

```java
// TODO 미사용 함수
public String getProgramName() {
     ...
     return nameOfProgram;
}
```

#### 4. 경고 주석
> 경고 주석은 잘못된 코드 사용을 방지하고 Side Effect(부작용)를 예방함

```java
 // WARN 암호화 모드 에서만 사용
 public void _getEncryptionResult() {
     ...
 }
```

### 1 - 3. 코드 복잡도 관리 (Function)
> 함수는 가급적 작게, 한번에 하나의 작업만 수행하도록 작성

#### 1. 간결한 코드
* 함수 인자 최소화 : 함수 인자를 최소화해 동작이 예측 가능하도록 함수를 작성함
* 중복 코드 제거 : 중복 코드를 제거해 가급적 적은 코드가 유지 되도록 함
* 죽은 코드 제거 : 더이상 사용하지 않는 함수는 삭제

#### 2. 역할이 분명한 코드
> 💡 **단일책임원칙**이란? 
클래스는 한가지 역할 만을 수행 하도록 한다.
이 원칙은 클래스 뿐 아니라 함수에도 동일하게 적용 가능함.

단일책임원칙을 지키다 보면, 
1. 분리된 각 클래스의 결합도(coupling)가 낮아지고 
2. 응집도(cohesion)가 높아져 
3. 외부 결합도(External coupling)는 낮추고 
4. 내용 결합도(Content coupling 또는 Pathological coupling)는 높인다.
→ 즉, **의존성을 최대한 줄여**야 한다!

예시 코드)
* 변경 전
```java
var vote_changed = function (old_vote, new_vote) {
    
	var score = get_score();
    
	if (new_vote !== old_vote) {
		if (new_vote == 'Up') {
			score += (old_vote === 'Down' ? 2 : 1);
		} else if (new_vote == 'Down') {
			score -= (old_vote === 'Up' ? 2 : 1);
		} else if (new_vote == '') {
			score += (old_vote === 'Up' ? -1 : 1);
		}
	}
	set_score(score);
    
};
```

* 변경 후
```java
var vote_value = function (vote) {
    
    if(vote === 'Up') {
        return +1;
    }
    if(vote === 'Down') {
        return -1;
    }
    return 0;
    
};

var vote_changed = function (old_vote, new_vote) {
    
    var score = get_score();
    
    score -= vote_value(old_vote); // 이전 값 제거
    score += vote_value(new_vote); // 새로운 값 더함
    set_score(score);
};
```


#### 3. 형식을 갖춘 코드
1. 적절한 행 길이
	* 큰 파일 보다 작은 파일이 이해하기 쉬움
    * 함수도 최대한 작게 만든다. 한 함수당 3~5줄 정도로 줄이는 것이 좋음
2. 형식 길이
	* 한 줄당 80~120자 정도의 길이로 제한하고 적절한 들여쓰기를 고려함
3. 적절한 배치
	* 서로 밀접한 개념은 한 파일에 세로로 가까이 둔다.
    변수는 사용하는 위치에서 가장 근접한 위치에 선언함.

### 1 - 4. 흐름제어 만들기(Making control flow easy to read)
#### 1. 왼쪽에는 변수를, 오른쪽에는 상수를 두고 비교
```java
if(length >= 10)

while(bytes_received < bytest_expected)
```

#### 2. 부정이 아닌 긍정을 다루자
```java
if( a == b ) { // a!=b는 부정
	// same
} else {
	// different
}
```

#### 3. if/else를 사용하며, 삼항 연산자는 매우 간단한 경우만 사용

#### 4. do/while 루프는 피하자

---

## 2. 리팩토링(Refactoring)
### 2 - 0. 리팩토링이란?
> 프로그램의 외부 동작은 그대로 둔 채, 내부의 코드를 정리하면서 개선하는 것을 말함

**목적** : 소프트웨어를 더 이해하기 쉽고 수정하기 쉽게 만드는 것
```
리팩토링은 성능을 최적화시키는 것이 아니다.
코드를 신속하게 개발할 수 있게 만들어주고, 코드 품질을 좋게 만들어준다.
```
즉, 이해하기 쉽고, 수정하기 쉬우면? → 개발 속도가 증가!

### 2 - 1. 언제 필요할까?
* 메소드 정리 : 그룹으로 묶을 수 있는 코드, 수식을 메소드로 변경함
* 객체 간의 기능 이동 : 메소드 기능에 따른 위치 변경, 클래스 기능을 명확히 구분
* 데이터 구성 : 캡슐화 기법을 적용해 데이터 접근 관리 
(캡슐화 : 연관된 데이터와 함수를 함께 묶어 외부와 경계를 만들고 필요한 것만 밖으로 드러내는 과정)
* 조건문 단순화 : 조건 논리를 단순하고 명확하게 작성
* 메소드 호출 단순화 : 메소드 이름이나 목적이 맞지 않을 때 변경
* 클래스 및 메소드 일반화 : 동일 기능 메소드가 여러개 있으면 수퍼클래스로 이동

### 2 - 2. 리팩토링 예제
* 예제 1
```java
// 수정 전
public int getFoodPrice(int arg1, int arg2) {
    return arg1 * arg2;
}
```
→ 함수명 직관적 수정, 변수명을 의미에 맞게 수정
```java
// 수정 후
public int getTotalFoodPrice(int price, int quantity) {
    return price * quantity;
}
```

* 예제 2
```java
// 수정 전
public int getTotalPrice(int price, int quantity, double discount) {
    return (int) ((price * quantity) * (price * quantity) * (discount /100));
}
```
→ ```price * quantity```가 중복된다. 따로 변수로 추출하자
→ 할인율을 계산하는 부분을 메소드로 따로 추출하자
→ 할인율 함수 같은 경우는 항상 일정하므로 외부에서 건드리지 못하도록 private 선언
```java
// 수정 후
// 수정 전
public int getTotalFoodPrice(int price, int quantity, double discount) {
	
    int totalPriceQuantity = price * quantity;
    return (int) (totalPriceQuantity - getDiscountPrice(discount, totalPriceQuantity))
}

private double getDiscountPrice(double discount, int totalPriceQuantity) {
    return totalPriceQuantity * (discount / 100);
}
```
→ totalPriceQuantity를 getter 메소드로 추출이 가능하다.
→ 지불한다는 의미를 주기 위해 메소드 명을 수정해주자
```java
// 수정 후
public int getFoodPriceToPay(int price, int quantity, double discount) {
    
    int totalPriceQuantity = getTotalPriceQuantity(price, quantity);
    return (int) (totalPriceQuantity - getDiscountPrice(discount, totalPriceQuantity));
}

private double getDiscountPrice(double discount, int totalPriceQuantity) {
    return totalPriceQuantity * (discount / 100);
}

private int getTotalPriceQuantity(int price, int quantity) {
    return price * quantity;
}
```

### 2 - 3. 클린코드와 리팩토링의 차이?
> 클린코딩 ⊂ 리팩토링

| 클린코드 | 리팩토링 |
| --- | --- |
| 가독성 높임 | 클린코드 + 유지보수 |
| 설계 시 | 결과물이 나온 이후 |

---

## 3. 시큐어코딩(Secure Coding)
### 3 - 0. 시큐어코딩이란?
> 안전한 소프트웨어를 개발하기 위해, 소스코드 등에 존재할 수 있는 잠재적인 보안약점을 제거함

### 3 - 1. 보안 약점을 노려 발생하는 사고사례들
* SQL 인젝션 취약점으로 개인유출 사고 발생
(SQL Injection : 악의적인 사용자가 보안상의 취약점을 이용하여, 
임의의 SQL 문을 주입하고 실행되게 하여 데이터베이스가 비정상적인 동작을 하도록 조작하는 행위)
* URL 파라미터 조작 개인정보 노출
* 무작위 대입공격 기프트카드 정보 유출

### 3 - 2. SQL 인젝션 예시
* 안전하지 않은 코드
```java
String query "SELECT * FROM users WHERE userid = '" + userid + "'" + "AND password = '" + password + "'";

Statement stmt = connection.createStatement();
ResultSet rs = stmt.executeQuery(query);
```

* 안전한 코드
```java
String query "SELECT * FROM users WHERE userid = ? AND password = ?";

PrepareStatement stmt = connection.prepareStatement(query);
stmt.setString(1, userid);
stmt.setString(2, password);
ResultSet rs = stmt.executeQuery();
```
→ 적절한 검증 작업이 수행되어야 안전함
→ 입력받는 값의 변수를 ```$``` 대신 ```#```을 사용하면서 바인딩 처리로 시큐어 코딩이 가능함 

