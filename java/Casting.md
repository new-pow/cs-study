## 캐스팅이란?

> **타입을 변환하는 것**을 말하며 형변환이라고도 한다.

- 자바의 상속 관계에 있는 부모와 자식 클래스 간에는 서로 간의 형변환이 가능

<br>

## 형변환의 종류

### 1. 묵시적 형변환

> **자식 클래스의 객체가 부모 클래스 타입으로 형변환 되는 것** (업캐스팅)

```java
// 예제 1

Parent p = new Child(); // (Parent) new Child()할 필요가 없음
```
→ Parent를 상속받은 Child는 Parent의 속성을 포함하고 있기 때문

<br>

```java
// 예제 2

class Person{
	String name;

	public Person(String name) {
		this.name = name;
	}
}

class Student extends Person{
	
	String age;
	
	public Student(String name) {
		super(name); // super 키워드에 대해서는 따로 설명하겠다.
	}
}
public class CastingTest {
	public static void main(String[] args) {
    
    	// student 참조변수를 이용하면 age, name에 접근 가능하다.
    	Student student = new Student("도리도리"); 
	
    	// person 참조변수를 이용하면 Student 객체의 멤버 중에서 Person 클래스의 멤버에만 접근이 가능하다.
        Person person = student; // "업 캐스팅"

        person.name = "세진세진";
        person.age = "24"; // 컴파일 오류 ~!
	
	}
}
```
→ `person`참조변수는 Student 객체를 가리킨다.
→ 하지만 Person 타입이므로 Person 클래스에 속한 멤버만 접근 가능하다.
→ person.age를 했을 때 컴파일 오류가 나는것이 바로 그 예시이다.
<br>

※ **super()**
* 부모 클래스의 생성자를 호출하는 메서드
* 자식 클래스의 인스턴스를 생성하면, 자식 클래스의 고유 멤버 뿐 아니라 부모 클래스의 모든 멤버까지 포함됨
* 부모 클래스의 멤버를 초기화하기 위해서는 `자식 클래스의 생성자에서 부모 클래스의 생성자까지 호출해야 한다.`

<br>
<br>

### 2. 명시적 형변환

> **부모 클래스가 자식 클래스 타입으로 캐스팅 되는 것** (다운캐스팅).
즉, 업캐스팅된 것을 다시 원상태로 돌리는 것.

```java
// 예제 1

Parent p = new Child();
Child c = (Child) p;
```
→ 다운캐스팅은 업캐스팅이 발생한 이후에 작용한다.
→ 하위 클래스로의 다운캐스팅을 할때는 타입을 **명시적으로 지정**해줘야 한다.

<br>

```java
// 예제 2

class Person{
	String name;
	
	public Person(String name) {
		this.name = name;
	}
}

class Student extends Person{
	
	String age;
	
	public Student(String name) {
		super(name); 
	}
}

public class CastingTest2 {
	public static void main(String[] args) {
		// 업 캐스팅 선행
		Person person = new Student("박세연");
		
		// 다운 캐스팅
		Student student = (Student) person;
		
		// name에 접근. student 타입이니까 전부 접근 가능
		student.name = "세욘이";
		
		// age에 접근
		student.age = "27";
	}
}
```

<br>

---

## 출처

- [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Language/[java] Casting(업캐스팅 %26 다운캐스팅).md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Language/%5Bjava%5D%20Casting(%EC%97%85%EC%BA%90%EC%8A%A4%ED%8C%85%20%26%20%EB%8B%A4%EC%9A%B4%EC%BA%90%EC%8A%A4%ED%8C%85).md)
- [https://computer-science-student.tistory.com/335](https://computer-science-student.tistory.com/335)
- [https://velog.io/@sezzzini/Java-Casting](https://velog.io/@sezzzini/Java-Casting)