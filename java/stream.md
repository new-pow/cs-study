※ Java 8버전 이상부터 Stream API 지원

## 스트림 Streams이란?

> 람다를 활용할 수 있는 기술 중 하나.

```
※ Java 8 이전    

배열 또는 컬렉션 인스턴스를 다루는 방법 :   
**for** 또는 **foreach** 문을 돌면서 요소 하나씩을 꺼내서 다루는 방법  

문제는?  
→ 간단한 경우라면 상관없지만,  
로직이 복잡해질수록 코드의 양이 많아져 여러 로직이 섞이게 되고,  
메소드를 나눌 경우 루프를 여러 번 도는 경우가 발생
```

반면, **스트림**은 '데이터의 흐름’이다.

→ 컬렉션에 저장되어 있는 엘리먼트들을 하나씩 순회하면서 처리할 수 있는 코드 패턴.

→ 람다식과 함께 사용되어 컬렉션에 들어있는 데이터에 대한 처리를 매우 간결한 표현으로 작성 가능.

→ 내부 반복자를 사용하기 때문에 병렬처리가 쉽다.

※ 병렬처리 : 하나의 작업을 둘 이상의 작업으로 잘게 나눠 동시에 진행하는 것.

즉, 쓰레드를 이용해 많은 요소들을 빠르게 처리 가능.

### ※ 자바 컬렉션(Collection)

| 인터페이스 | 구현클래스 |
| --- | --- |
| Set | HashSet   TreeSet |
| List | LinkedList   Vector   ArrayList |
| Queue | LinkedList   PriorityQueue |
| Map | Hashtable   HashMap   TreeMap |

### Collection vs Stream

1\. 차이점 : **데이터 계산 시점**

| Collection | Stream |
| --- | --- |
| 모든 값을 메모리에 저장.   따라서 Collection에 추가하기 전, 미리 계산 완료되어야 함. | 요청할 때만 요소를 계산하는 고정된 자료구조 |
| 외부 반복을 통해 사용자가 직접 반복 작업을 거쳐 요소를 가져올 수 있음 (for-each) | 내부 반복을 사용하므로, 추추루 요소만 선언해주면 알아서 반복 처리를 진행. |
|   | 스트림에 요소를 따로 추가 혹은 제거하는 작업은 불가능. |
| _핸드폰에 음악 파일을 미리 저장하여 재생하는 플레이어_ | _필요할 때 검색해서 듣는 멜론과 같은 음악 어플_ |

2\. 반복의 일회성

| Collection | Stream |
| --- | --- |
| 여러번 반복 처리 가능 | 단 한번만 반복문 처리 가능   (∵ 소비(Consumer) 개념을 쓰기 때문에,    한번 소비한 요소에 대해 접근할 수 없음) |

```
Stream<Food> s = foodList.stream();
s.forEach(System.out::println); // 정상
s.forEach(System.out::println); // IllegalStateException 발생
```

🚨 만약 위 코드를 실행한다면 

**stream has already been operated upon or closed** 라는 에러와 함께 프로그램이 중단됨.

### 외부 반복 & 내부 반복

→ 성능 면에선, '내부 반복'이 비교적 좋다.

| 외부 반복 | 내부 반복 |
| --- | --- |
| 명시적으로 컬렉션 항목을 하나씩 가져와서 처리   (최적화 불리) | 작업을 병렬 처리하면서 최적화된 순서로 처리 |
| Collection에서 병렬성 이용 :    직접synchronized를 통해 관리    |   |

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbg3Uh3%2FbtrUBaBPwR4%2FzbkKsJ9gKXvHW7ZMw5xdfk%2Fimg.png)

예제 밑에... 

---

## 스트림의 등장

```
컬렉션 데이터를 선언형으로 쉽게 처리 가능.  
 
복잡한 루프문을 사용하지 않아도 되며  
루프문을 중첩해서 사용해야 되는 최악의 경우도 더이상 없어졌다.
```

#### 예제 (스트림 사용 X vs 스트림 사용 O)

조건

1.  빨간색 사과 필터
2.  무게순서대로 정렬
3.  사과들의 고유번호 출력

**\[스트림 사용 X\]**

> 스트림을 사용하지 않을때는 각 필터링 단계마다 코드를 작성해야함.

```java
// 빨간색 사과 필터링
List<Apple> redApples = forEach(appleList, (Apple apple) -> apple.getColor().equals("RED"));

// 무게 순서대로 정렬
redApples.sort(Comparator.comparing(Apple::getWeight));

// 사과 고유번호 출력
List<Integer> redHeavyAppleUid = new ArrayList<>();
for (Apple apple : redApples)
    redHeavyAppleUid.add(apple.getUidNum());
```

**\[스트림 사용 O\]**

> 스트림을 사용하여 단 한줄로 표현 할 수 있음.

```java
List<Integer> redHeavyAppleUid = appleList.stream()
        .filter(apple -> apple.getColor().equals("RED")) // 빨간색 사과 필터링
        .sorted(Comparator.comparing(Apple::getWeight)) // 무게 순서대로 정렬
        .map(Apple::getUidNum).collect(Collectors.toList()); // 사과 고유번호 출력
```

또한 스트림은 **paralleStream** 메서드를 통해 별도의 멀티스레드 구현 없이도 병렬처리가 가능하다.

```java
List<Integer> redHeavyAppleUid = appleList.parallelStream() // 병렬 처리
        .filter(apple -> apple.getColor().equals("RED")) // 빨간색 사과 필터링
        .sorted(Comparator.comparing(Apple::getWeight)) // 무게 순서대로 정렬
        .map(Apple::getUidNum).collect(Collectors.toList()); // 사과 고유번호 출력
```

예제에서 사용한 filter, sorted, map 같은 함수들은 Steam API 에서 제공하는 함수들입니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FpdD45%2FbtrUKl9oLEz%2FEtPzJdkmRTiEPN9mLLJkk1%2Fimg.png)

## 스트림 API의 특징 정리

-   선언형 : 더 간결하고 가독성이 좋아진다.
-   함수의 조립 : 유연성이 좋아진다.
-   병렬화 : 성능이 좋아진다.

---

## 스트림(Stream) 시작해보기

예제에 사용할 Collection 미리 정의

List<Food>

```java
List<Food> foodList = new ArrayList<>();

foodList.add(new Food("FlatBread",true,400,Food.Type.OTHER));
foodList.add(new Food("OnionSoup",true,300,Food.Type.OTHER));
foodList.add(new Food("LobsterRisotto",false,520,Food.Type.FISH));
foodList.add(new Food("CaesarSalad",true,200,Food.Type.OTHER));
foodList.add(new Food("BeefWellington",false,670,Food.Type.MEAT));
foodList.add(new Food("FiletMignon",false,600,Food.Type.MEAT));
foodList.add(new Food("CrispySalmon",false,620,Food.Type.FISH));
foodList.add(new Food("StripSteak",false,740,Food.Type.MEAT));
foodList.add(new Food("SearedScallops",false,340,Food.Type.FISH));
```

\[Food.java\]

```java
import java.lang.reflect.Type;

public class Food {

    public enum Type {
        MEAT,
        FISH,
        OTHER
    }

    private final String name;
    private final boolean isVegetarian;
    private final int calories;
    private final Type type;

    public Food(String name, boolean isVegetarian, int calories, Type type) {
        this.name = name;
        this.isVegetarian = isVegetarian;
        this.calories = calories;
        this.type = type;
    }

    public String getName() {
        return name;
    }

    public boolean isVegetarian() {
        return isVegetarian;
    }

    public int getCalories() {
        return calories;
    }

    public Type getType() {
        return type;
    }
}
```

예제 코드 만들기

```java
List<String> highCaloriesFoodName = foodList.stream()
        .filter(food -> food.getCalories() > 400)
        .map(Food::getName)
        .limit(3)
        .collect(Collectors.toList());

System.out.println(highCaloriesFoodName);
```

→ 1. stream() 함수를 통해 foodList라는 **소스(Source)**로부터 연속된 요소를 얻어 스트림을 만들고

→ 2. 해당 스트림에 Stream API 함수인 filter, map, limit, collect로 이어지는 데이터 처리 연산을 적용

→ 3. collect를 제회한 filter, map, limit 연산은 파이프라인을 형성할 수 있도록 스트림을 반환 

(파이프라인은 데이터베이스의 SQL 질의문 같은 존재)

→ 4. 마지막으로 **collec**t 연산으로 파이프라인을 처리하여 결과를 반환

(단, collect는 스트림이 아닌 List를 반환)

```
※ 소스 (Source)  
스트림은 컬렉션, 배열, I/O 자원 등의 소스로부터 데이터를 소비하고  
정렬된 컬렉션으로 스트림을 생성하면 정렬이 그대로 유지됨.  
즉, 리스트로 스트림을 만들면 스트림의 요소는 리스트의 요소와 같은 순서를 유지.
```

```
※ 데이터 처리 연산  
filter, sort, map, match 등으로 데이터를 조작할수 있고 순차적 혹은 병렬로 실행할수 있다.
```

```
※ 파이프라이닝과 내부 반복 (스트림의 중요한 특징)  
 
1. 파이프라이닝 (Pipelining)  
- 스트림 연산들은 서로 연결하여 큰 파이프라인을 구성할 수 있도록 스트림 자신을 반환한다.  

2. 내부 반복  
- 반복자를 이용하여 명시적으로 반복하는 컬렉션과 다르게 스트림은 내부 반복 기능을 제공.
```

---

### 외부 반복, 내부 반복 예제

Food 리스트의 이름들을 추출하는 코드를 컬렉션과 스트림 두가지 방법으로 구현

#### **\[컬렉션\]**

```java
List<String> foodNameList = new ArrayList<>();
for(Food food : foodList){
    foodNameList.add(food.getName());
}
```

#### **\[스트림\]**

```java
List<String> foodNameList = foodList.stream()
        .map(Food::getName)
        .collect(Collectors.toList());
```

→ 컬렉션과 다르게 스트림은 별도의 반복자 없이도 반복문을 처리할 수 있다.

스트림이 사용하는 내부 반복의 장점은 

작업을 병렬로 처리할 수 있고, 더 최적화된 다양한 순서로 처리할 수 있다는 점.

---

## 스트림(Stream) 연산

> 스트림은 연산 과정이 '중간'과 '최종'으로 나누어짐

1.  중간 연산 : 파이프라인으로 연결할 수 있는 연산들 (filter, map, limit 등)
2.  최종 연산 : 파이프라인을 실행한 다음 닫는 연산 (count, collect 등)

※ 나누는 이유 : 중간 연산들은 스트림을 반환해야 하는데,

모두 한꺼번에 병합하여 연산을 처리한 다음 최종 연산에서 한꺼번에 처리하게 됨.

```java
List<String> highCaloriesFoodName = foodList.stream()
        .filter(food -> food.getCalories() > 400) // 중간연산
        .map(Food::getName) // 중간연산
        .limit(3) // 중간연산
        .collect(Collectors.toList()); // 최종연산

// filter와 map은 다른 연산이지만, 한 과정으로 병합된다.
```

위 예제코드를 보면 

filter, map, limit는 중간연산이고, collect는 최종연산이다.

---

### 중간 연산

> filter나 map 같은 중간 연산은 다른 스트림을 반환하기 때문에  
> 여러 개의 중간연산을 연결하여 질의를 만들 수 있다.  
>   
> 중요한 특징은 최종 연산을 실행하기 전까지는 아무 연산도 수행하지 않는다는 것이다.

#### Stream 중간 연산 종류

> 중간 연산은 모두 스트림을 반환한다.

-   filter(Predicate) : Predicate를 인자로 받아 true인 요소를 포함한 스트림 반환
-   distinct() : 중복 필터링
-   limit(n) : 주어진 사이즈 이하 크기를 갖는 스트림 반환
-   skip(n) : 처음 요소 n개 제외한 스트림 반환
-   map(Function) : 매핑 함수의 result로 구성된 스트림 반환
-   flatMap() : 스트림의 콘텐츠로 매핑함. map과 달리 평면화된 스트림 반환

#### 중간 연산 예제

스트림 파이프라인에서 연산이 어떻게 진행되는지 확인해보기 위해 연산에 출력문을 넣어 확인.

```java
List<String> highCaloriesFoodName = foodList.stream()
        .filter(food -> {
            System.out.println("filter : " + food.getName());
            return food.getCalories() > 400;
        })
        .map(food -> {
            System.out.println("map : " + food.getName());
            return food.getName();
        })
        .limit(3)
        .collect(Collectors.toList());

System.out.println(highCaloriesFoodName);
```

#### **\[출력\]**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcCaiwL%2FbtrUCizC74I%2FvuHwIgCEIqTHIlVfSJdSVK%2Fimg.png)

→ OnionSoup, CaesarSalad는 filter에서 필터링 되었기 때문에 map에서는 찍히지 않고

나머지 음식들이 최종연산되어 출력되는 것을 확인.

---

### 최종 연산

> 파이프라인 연산의 결과를 출력

#### 최종 연산 종류

-   (boolean) allMatch(Predicate) : 모든 스트림 요소가 Predicate와 일치하는지 검사
-   (boolean) anyMatch(Predicate) : 하나라도 일치하는 요소가 있는지 검사
-   (boolean) noneMatch(Predicate) : 매치되는 요소가 없는지 검사
-   (Optional) findAny() : 현재 스트림에서 임의의 요소 반환
-   (Optional) findFirst() : 스트림의 첫번째 요소
-   reduce() : 모든 스트림 요소를 처리해 값을 도출. 두 개의 인자를 가짐
-   collect() : 스트림을 reduce하여 list, map, 정수 형식 컬렉션을 만듬
-   (void) forEach() : 스트림 각 요소를 소비하며 람다 적용
-   (Long) count : 스트림 요소 개수 반환

---

## Stream 활용 예제들

1\. map()

```java
List<String> names = Arrays.asList("Sehoon", "Songwoo", "Chan", "Youngsuk", "Dajung");

names.stream()
    .map(name -> name.toUpperCase())
    .forEach(name -> System.out.println(name));
```

결과

```
SEHOON
SONGWOO
CHAN
YOUNGSUK
DAJUNG
```

2\. filter()

```java
List<String> names = Arrays.asList("Sehoon", "Songwoo", "Chan", "Youngsuk", "Dajung");

List<String> startsWithN = names.stream()
    .filter(name -> name.startsWith("S"))
    .collect(Collectors.toList());

System.out.println(startsWithN);
```

결과

```
[Sehoon, Songwoo]
```

3\. reduce()

```java
Stream<Integer> numbers = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
Optional<Integer> sum = numbers.reduce((x, y) -> x + y);
sum.ifPresent(s -> System.out.println("sum: " + s));
```

결과

```
sum: 55
```

4\. collect()

```java
List<String> names = Arrays.asList("Sehoon", "Songwoo", "Chan", "Youngsuk", "Dajung");

System.out.println(names.stream()
                   .map(String::toUpperCase)
                   .collect(Collectors.joining(", ")));
```

결과

```
SEHOON, SONGWOO, CHAN, YOUNGSUK, DAJUNG
```

---

## 스트림 이용하기 요약

스트림을 사용하는 단계는 다음과 같이 3단계에 걸쳐서 진행된다.

-   질의를 수행할 데이터소스
-   스트림 파이프라인을 구성할 중간 연산
-   스트림 연산을 실행하고 결과로 출력할 최종 연산

---

### 출처

-   [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Language/%5Bjava%5D%20Stream.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Language/%5Bjava%5D%20Stream.md)
-   [https://futurecreator.github.io/2018/08/26/java-8-streams/](https://futurecreator.github.io/2018/08/26/java-8-streams/)
-   [https://hbase.tistory.com/171](https://hbase.tistory.com/171)
-   [https://gangnam-americano.tistory.com/41](https://gangnam-americano.tistory.com/41)
-   [https://ksr930.tistory.com/237](https://ksr930.tistory.com/237)