## **람다식 Lambda Expression**

-   함수(메서드)를 간단한 ‘식’으로 표현하는 방법이다.

```
(a, b) -> a>b ? a: b
```

-   익명 함수 anonymous function
-   함수와 메서드의 차이점
    -   근본적으로 동일하지만,
        -   함수 : 일반적인 용어. 클래스에 독립적
        -   메소드 : 객체지향개념의 용어이다. 클래스에 종속적이다.

### [](https://gist.github.com/new-pow/0db33048036b267f54db4ad712f6503b#%EB%9E%8C%EB%8B%A4%EC%8B%9D-%EC%82%AC%EC%9A%A9%EB%B2%95)**람다식 사용법**

-   호출해서 사용하는 방식이 아닌, 구현부에서 바로 함수처리를 하여 내부에서 직접 기능을 처리하는 방식

1.  반환 타임과 이름을 지운다. ()와 {} 사이에 화살표로 연결한다.
2.  반환값이 있는 경우 식이나 값만 적고 return, ; 생략 가능
3.  매개변수의 타입이 추론 가능하면 대부분 생략 가능하다.

```
// 작성실습
int max(int a, int b) {
	return a>b? a:b;
}
```

```
(a,b) -> a>b ? a : b
```

-   람다 사용시 반드시 함수형인터페이스를 먼저 정의해야 한다.

### **함수형 인터페이스**

-   **단 하나의 추상 메서드**만 선언된 인터페이스
-   @FunctionalInterface 를 클래스에 붙여준다.
    -   없어도 되지만, 클라이언트에게 함수형 인터페이스를 표현할 수 있으며 조건 충족을 검사할 수 있다.
    -   조건에 충족하지 않으면 컴파일 에러가 발생한다.

```
**@FunctionalInterface**
interface MyFuntion{
	public abstract int max(int a, int b);
}
```

```
MyFunction f = new MyFunction() { // 사용 방법
		public int max(int a, int b) {
			return a>b ? a:b;	
		}
	}

// 람다식을 참조할 수 있다.
MyFunction f = (a,b) -> a>b ? a:b;

int value = f.max(3,5); //
```

-   Java에서 자주 사용되는 함수형 인터페이스 java.util.function
    -   표 외에도 더 많다. [공식문서 참고자료](https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html)

| **Function<T, R>** | T -> R |
| --- | --- |
| **BiFunction<T,U,R>** | T,U -> R |
| **Consumer** | T -> () |
| **Supplier** | () -> T |
| **Predicate** | T -> boolean |
| **UnaryOperator** | Function<T,T> 와 같음. T -> T |
| **BinaryOperator** | BiFunction<T,T,T>와 같음. T, T -> T |

### [](https://gist.github.com/new-pow/0db33048036b267f54db4ad712f6503b#%EC%A3%BC%EC%9D%98%EC%82%AC%ED%95%AD)**문법**

-   매개변수가 1개인 경우, 타입 없다면 생략 가능
-   블록 안에 문장이 하나라면 {} 생략 가능. 끝에 ; 안 붙여도 된다.

### [](https://gist.github.com/new-pow/0db33048036b267f54db4ad712f6503b#%EB%9E%8C%EB%8B%A4%EC%8B%9D%EC%9D%98-%ED%8A%B9%EC%A7%95)**람다식의 특징과 장점**

-   **익명 함수**
    -   특정 클래스에 종속되지 않는 함수이다.
-   **익명 객체Object이다.**
    -   자바에서는 메소드만 존재할 수 없으니까 이를 객체로 다루기 위해선 함수형 인터페이스가 필요하다.
-   **전달이 가능하다.**
    -   람다 표현식을 메서드 인수로 전달하거나 변수로 저장할 수 있다.
-   **간결해져 가독성이 향상된다.**
-   **멀티 스레드 환경에서 용이하다.** (함수형 프로그래밍의 특징)

### [](https://gist.github.com/new-pow/0db33048036b267f54db4ad712f6503b#%EB%9E%8C%EB%8B%A4%EC%9D%98-%EB%8B%A8%EC%A0%90)**람다의 단점**

-   람다로 인한 무명함수는 재사용이 불가능하다. (항상 새 인스턴스로 할당해야 한다.)
-   디버깅이 좀 힘들다.
-   무분별한 람다 사용은 코드 가독성을 해친다.
-   재귀로 만들기 부적합하다.