# 메모리 할당에 대한 이해

December 19, 2022 

# 메모리 할당

- 어떠한 변수를 선언하면 메모리가 할당된다.
- 변수를 선언하기 위해 할당되는 메모리로는 크게 스택과 힙이 있다.

## 스택 Stack

- 함수의 호출과 함께 지역 변수, 매개변수 등이 할당.
- 정렬된 방식으로 메모리가 할당되고 해제된다.
- **실제 값들이 저장되는 것.**

## 힙 Heap

- 클래스 변수(혹은 인스턴스 변수)또는 객체 등이 할당된다.
- 우연하고 무질서하게 메모리가 할당된다.
- JVM이 가비지 컬렉터를 통해 메모리 해제를 관리한다.

```java
public void test() {
    // Primitive Value
    int x = 3;
    float y = 10.012f;
    boolean isTrue = true;
}
```

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F84731898-119a-4e46-8ba0-67a20055b6ee%2FUntitled.png?id=95088145-992b-4de2-b51d-c2be50f1a4b9&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

```java
public void test() {
    // Primitive Value
    int x = 3;
    float y = 101.012f;
    boolean isTrue = true;
    
    // Object
    String name = "MangKyu";
    
    String[] names = new String[3];
    names[0] = "I";
    names[1] = "am";
    names[2] = "MangKyu";
    
}
```

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F8ecfb04c-9710-48e2-8112-c1d1a3615f1a%2FUntitled.png?id=49befc7e-128f-405f-aa9d-f90be08b0238&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)
---

- 참고
    
    - [[Java] 메모리 관리 및 Pass By Value의 동작 방식 (2/3)](https://mangkyu.tistory.com/106)

- 연관
	- [Call by value, Call by reference](./Call_by_value-Call_by_reference)