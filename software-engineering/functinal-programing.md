-   **함수형 프로그래밍은 애플리케이션, 함수의 구성요소, 더 나아가서 언어 자체를 함수처럼 여기도록 만들고, 이러한 함수 개념을 가장 우선순위에 놓는다.**
    -   함수형 사고방식은 문제의 해결 방법을 동사(함수)들로 구성(조합)하는 것
    -   마이클 포거스 [클로저 프로그래밍의 즐거움]
-   성공적인 프로그래밍을 위해 **부수 효과를 미워**하고 **조합성을 강조**하는 프로그래밍 패러다임
    -   순수함수를 만든다.
    -   모듈화 수준을 높인다.
-   Avoids changing State and Mutable data
    -   상태와 Data 변경하는 것을 피하면서 프로그래밍
-   Functional Programming is programming without assignment satements

### ？ 함수형 프로그래밍에 대한 오해

-   OOP 와 반대되는 개념은 아니다. 오히려 OOP를 잘 알아야 함수형 프로그래밍도 잘 할 수 있다.

## 함수형 프로그래밍과 객체지향 프로그래밍의 차이점

```java
// 데이터(객체) 기준
dog.moveLeft();
cat.moveLeft();
dog.moveRight();

// 함수 기준
moveLeft(dog);
moveRight(cat);
moveLeft({x:5, y:2});
```

-   객체지향 프로그래밍
    -   데이터를 먼저 만들고 함수 구성
-   함수형 프로그래밍
    -   함수를 만들고 그에 맞는 데이터 셋을 구성

# 함수형 프로그래밍의 특징

1.  불변 객체를 사용한다.
2.  참조 투명성을 가진다.
3.  실제로 필요해지는 경우에 연산을 시작한다.
4.  코드를 간결하게 해준다.
5.  에러가 없기 때문에 병렬처리하기 좋다.

## Immutable DataStructure 불변 객체

-   반대 : Mutable
-   `java` 에서 `final` 과 같음.

```kotlin
val immutableList : List<Int> = listOf(1,2,3)
immutableList.add(10) // error

immutableList.plus(10) // not error
println(immutableList) // [1,2,3]
println(immutableList.plus(10) // [1,2,3,10]

var newList : immutableList.plus(10)
println(innutableList) // [1,2,3]
println(newList)       // [1,2,3,10]
```

-   **자료구조 수정을 할때 원본은 변화지 않고 수정을 통해 새로운 객체를 반환한다.**
-   값이 변하지 않기 때문에 내가 몇 번을 참조해도 값이 변하지 않는다.

## Pure Function 순수함수

-   참조 투명성

```kotlin
fun main(args: Array<String>) {
	println(pureFunction("FP")  // Hello FP
	println(pureFunction("FP")  // Hello FP
	println(pureFunction("FP")  // Hello FP
}

fun pureFunction (iniput: String): String {
	return "Hello " + input
}
```

-   **언제 몇 번을 호출하든 input이 같다면 output이 같다.**
-   0개 이상의 인수를 가지고, 한 개이 상의 결과를 반환하며 **부수효과**가 없다.
    -   no side effect
        -   자료구조를 고치거나 필드값에 할당
        -   자료구조를 제자리에서 수정함
        -   예외 발생, 오류로 실행 중단
        -   파일에 쓰기 등의 I/O 동작 수행

### 비순수 함수의 경우

```kotlin
fun main(args: Array<String>) {
	println(nonPureFunction("FP")  // Hello FP
	println(nonPureFunction("FP")
	println(nonPureFunction("FP")
}

val strBuilder: StringBuilder = StringBuilder("Hello ")

fun nonPureFunction(input: String): String {
	return strBuilder.append(input).toString()
}
```

-   출력값이 여러번 호출하면 달라진다.
-   동시성을 생각했을 때 (멀티스레드) 굉장히 프로그래밍이 복잡해진다. → 에러를 정확히 확인 못할 수도 있다.
-   테스트 코드를 작성하기 힘들다.

```kotlin
var x =1

fun nonPureFunction2(input: Int): Int{
	return input+x
}
```

-   **외부 변수를 참조한다면 순수 함수가 아니다.**
    -   side effect가 있으므로
-   변수가 언제 바뀔지 모르기 때문에 순수함수가 아니다.

## Lazy evaluation 게으른 평가

```kotlin
val lazyValue2: () -> Unit = {
	println("FP")
}

lazyValue2   //
lazyValue2   //
lazyValue2   //
lazyValue2() // FP
```

-   → allow
    -   왼편 == input
    -   오른편 == output

---

# 함수형 자료구조 Functional Data Structure

-   불변 자료구조
-   순수함수 자료구조
-   자료 공유

```kotlin
fun main(args: Array<String>) {
	val value = 3
	val result = plusThree(value)

	println(result) // 6
	println(value) // 3
}

fun plusThree(x: Int): Int{
	return x+3
}
```

```kotlin
fun main(args: Array<String>) {
	val list = listOf(1,2)
	val listResult = plusThree(list)

	println(list) // 1,2
	println(listResult) // 1,2,3
}

fun plusThree(list: List<Int>): List<Int>{
	return list.plus(3)
}
```

-   이렇게 매번 변수가 바뀌면 비효율적이지는 않을까?
    -   자료 공유 Data Share

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/baa83109-7798-4531-ad3f-2a50b53a5333/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/22fcbdcb-6b77-4c83-8820-9e0dda7ea3b2/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d61c2c16-2d08-4cd8-9f0c-6df6b0114e25/Untitled.png)

-   원본 리스트를 반환을 하지만, 추가로 생성되는 것보다는 재활용하고 있다.
-   이를 자료공유라고 한다.

## 참조 : 재귀 Recursion

### 재귀를 사용할 때

-   어떻게 보다 무엇에 집중
-   종료조건부터 생각하자
-   재귀를 반복할 수록 종료 조건으로 수렴하도록 기획

```kotlin
fun factorial (num: Int): Int {
	return num*factorial(num-1)
}
```

### 재귀의 문제점 → 꼬리재귀

-   생각보다 효율적인 코드는 아니다.
-   Performance - SOF (스택오버플로우 생길 수 있다)

```kotlin
// TailRecursion
// 스택이 쌓이지 않고 라인대로 동작한다.

tailrec fun factorial3(num: Int, acc: Int=1): Int =
when (num) {
	1 -> acc
	else -> factorial3(num - 1, acc*num)
}
```

-   TailRecursion 꼬리재귀 를 통해 함수형 프로그래밍으로 실행 가능하다.
-   이렇게 하면 가독성 + 성능 + 스택오버플로우 발생하지 않는다.
-   상황에 따라 선택하면 된다.

---

# 함수형 프로그래밍이 다시 재발굴된 이유

-   좋아지는 하드웨어 성능
-   좋아지는 컴파일러
-   함수형 프로그래밍 기술의 발전
-   좋아지는 분산, 리액티브 환경
-   동시성 + 병렬성 관련 기술
-   성공적인 적용 사례와 영향

## Java 와 함수형 프로그래밍

Java 8부터 Java에서도 함수형 프로그래밍이 가능해졌다.

-   stream api
-   lamda
-   함수형 인터페이스

---

-   참고
    -   ****[함수형 프로그래밍이란 무엇이고? 어디에? 어떻게 쓸까? 1강 - 함수형 프로그래밍 개념](https://www.youtube.com/watch?v=V1u3aqV-qXg&t=95s&ab_channel=SKplanetTacademy)****
    -   [함수형 프로그래밍 개요](https://youtu.be/_eyDJzRy-KM)
    -   [함수형 프로그래밍](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Software%20Engineering/Fuctional%20Programming.md)