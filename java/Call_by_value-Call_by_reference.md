# 메서드 호출 시 파라미터를 전달하는 방법

## Call by Value

-   메서드를 호출할 때 값을 넘겨준다.
-   메서드를 호출하는 호출자 변수와 호출 당하는 수신자의 파라미터는 **복사된 서로 다른 변수.**
-   값만을 전달하기 때문에 수신자의 파라미터를 수정해도 호출자의 변수에는 아무런 영향이 없다.
-   **Java**

## Call by Reference

-   참조(주소)를 직접 전달한다.
-   호출자의 변수와 수신자의 파라미터가 **완전히 동일한 변수이다.**
-   메서드 내에서 파라미터를 수정하면 그대로 원본 변수에도 반영된다.
-   **C, C++**

# Java : Call by value

Java에서는 `Call by value` 를 사용한다.

## 예시를 통해 알아보는 Call by value

```java
public class Hello {
	public int money;
	public String name;

	public static void increase(int a) {
		a++;
		System,out.println("inside: "+a);
	}

	public static void give100Won(hello h) {
		h.money += 100;
	}

	public static void main(String[] args) {
		int m=9999;
		increase(m);
		System.out.println(m);
	}
}
```

-   main을 실행했을 때

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fe8fab9ad-3d4b-4893-a39b-5391357f6ec5%2FUntitled.png?id=88f609d7-cff1-4929-89ce-3cfdfc96e5fd&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F6f7206d7-ddd7-4ef7-b114-f81787e85197%2FUntitled.png?id=de87e4fd-296c-43f9-a6a7-925750b993ee&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F04e00004-228c-4b6a-9372-29169c1de101%2FUntitled.png?id=702388d6-8b26-4fca-84ea-ba6ee567448c&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

## 왜 헷갈리는걸까?

```java
public class Hello {
	public int money;
	public String name;

	public static void increase(int a) {
		a++;
		System,out.println("inside: "+a);
	}

	public static void give100Won(hello h) {
		h.money += 100;
	}

	public static void main(String[] args) {
		Hello h = new Hello();
		h.money = 100;
		give100Won(h);
		System.out.println("main "+h.money);
	}
}
```

-   참조타입의 경우, 주소값으로 저장된다.
    -   이 때문에 `call by reference`로 보이지만, 사실 다 똑같은 `call by value`이다.

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fed29f55a-83f2-40a9-bae8-2f4c010a57c7%2FUntitled.png?id=dd5cf0e7-575c-4ee5-8a7d-ae794cbf7b5c&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ffc355c5d-9765-4acd-a0ca-80ea762caa8f%2FUntitled.png?id=c2ca0ec2-17ea-43a8-a15b-a8113601734a&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

---

-   참고
- 연관글
	- [jvm 메모리 할당 방법](./jvm-stack-heap)