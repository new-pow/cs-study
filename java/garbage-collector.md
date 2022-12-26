# 가비지 컬렉터 Garbage Collector

-   프로그램이 **동적으로 할당한 메모리 영역** 중 **사용하지 않은 영역**을 탐지하여 해지하는 기능
-   동적으로 할당한 메모리 영역
    -   Stack : 정적으로 할당된 메모리 영역
        -   원시 타입의 데이터가 값과 함께 할당, Heap영역에 생성된 Object 타입의 데이터의 참조값 할당
    -   **Heap** : 동적으로 할당한 메모리 영역
        -   모든 Object 타입의 데이터가 할당. Heap영역의 Object를 가리키는 참조변수가 Stack에 할당된다.
-   사용하지 않는 영역
    -   어떤 변수도 가리키지 않음.

## Managed Language

-   ↔ Unmanaged Language
    -   C, C++ 에서는 메모리에서 직접 안쓰는 변수를 개발자가 지워줘야 했다.
    -   만약 제대로 지워주지 않으면 메모리 누수가 일어날 수 있다.
    -   거꾸로 해제했던 메모리를 다시 사용하는 등의 버그가 양산된다.
-   Java, Javascript는 자동으로 메모리가 관리되는 Managed Language 이다.
-   GC가 언어와 동작하는 환경마다 다르지만, 특정 때에 특정 방식으로 필요없는 정보들을 삭제한다.

## GC 장점

-   메모리 누수 가능성을 없앨 수 있다.
-   해제된 메모리에 접근을 하는 오류를 막는다.
-   해제한 메모리를 또 해제하는 오류를 막는다.

## GC 단점

-   GC작업은 순수 오버헤드 (프로그램의 일을 방해한다.)
-   개발자는 언제 GC가 메모리를 해제하는 지 모른다. (자동으로 실행되기 때문)
-   실시간성이 매우 강조되는 프로그램이라면 GC가 맞지 않을 수 있다.

---

## 자동 GC의 알고리즘

-   **Garbage Collection Roots**
    -   스택 변수, 전역 변수 등 heap영역 참조를 담은 변수
    -   지역변수, 활성 스레드, 정적 필드, JNI 참조

### Reference counting

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F98d55bcf-f35b-4c81-9c1b-d62101ae4fc1%2FUntitled.png?id=d4812e80-df62-409d-9e42-32af2c9fe8fa&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1920&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F8885d4d8-c8a8-42bf-ac6b-3496dde879a7%2FUntitled.png?id=4b9e3cea-35e0-435a-a742-11d6804cdeee&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1920&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

-   참조 카운팅
-   별도의 reference count 라는 별도 숫자를 가지고 있다.
-   한 요소가 다른 요소에게 몇 번 참조가 되는지 센 후
-   그 수가 0이 되면 치우는 것

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fcb3a31c2-e7a6-4a1e-b996-d527bf94f0ec%2FUntitled.png?id=3a36eaf4-c370-4d07-b356-2839c81299bb&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1920&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

-   단점은 서로 순환 참조하는 변수의 경우 서로를 1로 카운팅하므로 삭제되지 않는다는 점이 있다.

### Mark and sweep

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F5d4944a2-6711-4d47-945d-79669c773c67%2FUntitled.png?id=11587622-8033-4891-8f78-16f46ea00bc3&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1920&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

-   Root에서부터 해당 객체에 접근 가능한지를 해제의 기준으로 삼는다.
-   메모리를 훑으며 아직 필요한 것들만 마크한 다음 그 외의 것은 치워버린다.
-   1단계 : Mark
    -   GC 루트에서 시작하여 도달할 수 있는 모든 객체를 탐색하고 이러한 모든 객체에 대한 원장을 기본 메모리에 유지합니다.
-   2단계 : sweep
    -   도달할 수 없는 개체가 차지하는 메모리 주소를 다음 할당에서 재사용할 수 있도록 하는 것입니다.
    -   이 과정에서 `compaction`이 일어나기도 한다.

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F16c5e660-d256-44c9-90bd-7e47c0133a03%2FUntitled.png?id=5ae0b894-0499-414c-96de-bef9862c06ee&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1920&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fd7b724bb-b3c5-4ae2-9d62-7657576a2368%2FUntitled.png?id=dca3710d-20f1-49cb-97cf-04d16bbb14a7&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1920&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

-   장점
	- 더이상 사이클이 누출되지 않는다는 것이다.
-   단점
	- GC가 시행되기 위해 응용 프로그램 스레드를 중지해야 한다.
	    -   참조가 항상 변경되는 경우 실제로 참조를 계산할 수 없기 때문이다.
	    -   의도적으로 GC를 실행시켜야 한다.
	-   JVM이 정리작업에 몰두할수있도록 애플리케이션이 일시적으로 중지되는 상황을 Stop The World pause라고 한다.

---

## Java의 GC

-   `Mark and Sweep` 방식을 사용한다.

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F18d32c65-8328-4fb8-8d39-d27f053a437e%2FUntitled.png?id=583a315b-5f84-4b50-942f-d96fa87c07b1&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1920&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

-   **method area** : 프로그램의 클래스코드를 메타데이터로 가지고 있고, method들을 저장한다.
-   heap : 어플리케이션 실행되는 객체 인스턴스를 저장한다.
-   **stack** : 메서드 호출을 스택 프레임이라는 블록으로 쌓으며, 로컬변수, 중간 연산 결과들이 저장된다.
-   pc register : 스레드가 현재 실행할 스택 프레임의 주소를 저장하고 있다.
-   **native method stack**은 c, c++ low level 코드를 실행한다.

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F9c58d00f-32ef-4301-9630-ca4d9d3daea9%2FUntitled.png?id=c1062869-a4dc-4d82-850f-cdd0e18fd780&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1920&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

-   GC의 `root space`는 **method area, stack, native method stack** 이다.

## Heap 영역 살펴보기

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F07bf6c81-280e-466e-b099-8f89491f7f49%2FUntitled.png?id=7016917b-a333-437c-83dd-ce334f00dc50&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1920&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

-   Young Generation
    -   `minor gc`가 일어난다.
    -   3영역 으로 나뉜다.
-   Old Generation
    -   `major gc`가 일어난다.

## Young Generation

### eden

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F93abc04b-c622-4340-b9f1-e5039fa93a8a%2FUntitled.png?id=0c4ad8d1-5ac6-4235-a40c-878252fc1825&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1920&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

-   **Eden은 객체가 생성될 때 일반적으로 객체가 할당되는 메모리 영역**
-   일반적으로 동시에 많은 객체를 생성하는 여러 스레드가 있으므로 Eden은 Eden 공간에 상주하는 하나 이상의  **스레드 로컬 할당 버퍼**  (TLAB)로 더 나뉜다.
-   이러한 버퍼를 통해 JVM은 다른 스레드와의 비용이 많이 드는 동기화를 피하면서 해당 TLAB에서 직접 하나의 스레드 내에서 대부분의 개체를 할당할 수 있다.
-   TLAB 내부 할당이 불가능한 경우(일반적으로 충분한 공간이 없기 때문에) 공유 Eden 공간으로 할당이 된다.
-   **공간이 충분하지 않으면 더 많은 공간을 확보하기 위해 Young Generation에서 GC 프로세스가 트리거된다.**
-   마킹단계에서 **reachable** 한 모든 개체를 마크한다.
-   스윕단계에서 모든 마크된 개체가 Survivor 공간 중 하나로 복사된다. Eden은 빈다.
-   **`Mark and Copy`**

### Survivor

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fae429021-b8db-4737-af06-055c351c1bb3%2FUntitled.png?id=9de969bb-9adc-4375-8ae6-13bb87d4295c&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1920&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

-   `minor gc`로부터 살아남은 객체들이 존재하는 영역
-   두 개의 Survivor 공간 중 하나는 항상 비어있다.
-   `age bit`가 일정수준 이상 넘어가면 `Old generation`으로 이동한다. == `Promotion`

## Old Generation

-   `Old Generation`은 일반적으로 훨씬 더 크며 가비지가 될 가능성이 적은 객체가 차지한다.
-   Old Generation의 GC는 Young Generation보다 덜 자주 발생한다.
-   대부분의 개체는 Old Generation에서 살아 있을 것으로 예상되므로 표시 및 복사가 발생하지 않는다. 대신 조각화를 최소화하기 위해 개체를 이동한다.
-   **`major GC`의 알고리즘**
    -   GC 루트를 통해 액세스할 수 있는 모든 객체 옆에 표시된 비트를 설정하여 도달 가능한 객체를 표시
    -   도달할 수 없는 모든 개체 삭제
    -   라이브 개체를 Old 공간의 시작 부분에 연속적으로 복사하여 이전 공간의 내용을 압축

### PermGen

-   Java 8 이전에는 `Permanent Generation`이라는 특별한 공간이 있었다. 이것은 클래스와 같은 메타 데이터가 저장되는 곳. 내부화된 문자열과 같은 일부 추가 사항도 보관되었다.
-   예측이 어렵기 때문에 개발자에게 에러가 생겼다. : [java.lang.OutOfMemoryError: Permgen space](https://plumbr.io/outofmemoryerror/permgen-space)
-   이 문제를 해결하는 방법은 허용되는 최대 permgen 크기를 256MB로 설정하는 다음 예제와 유사하게 permgen 크기를 늘리는 것

### → 메타스페이스

-   java 8 이후부터는 대부분의 항목이 java heap에 저장되게 된다.
-   클래스 정의는 이제 `Metaspace`라는 항목에 로드
-   기본 메모리에 있으며 일반 힙 개체를 방해하지 않는다.
-   너무 커지면 오류를 야기할 수 있으므로 크기를 256MB로 설정

## 왜 이렇게 설계했을까?

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F681052d0-bcdf-4bdb-8f93-ae5cce75db9d%2FUntitled.png?id=a84a8062-b1a9-47d7-8948-d09e4841babd&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1920&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

-   대부분의 개체는 빠르게 사용되고 삭제된다.
-   일반적으로 (매우) 오랫동안 생존하지 못하는 것
-   GC 알고리즘은 '어려서 죽거나' '영원히 살 가능성이 있는' 객체에 최적화되어 있기 때문에 JVM은 '중간' 기대 수명을 가진 객체에서 제대로 작동하지 않는다.

## JVM GC 실행 방식

### Stop the world

-   GC를 실행하기 위해 JVM이 애플리케이션 실행을 멈추는 것
-   이 시간을 최소화해야한다.

### 방식1 : Serial GC 직렬화 GC

-   하나의 쓰레드로 GC를 실행
-   Young Generation에 대해 **[mark-copy](https://plumbr.io/handbook/garbage-collection-algorithms/removing-unused-objects/copy)** 사용. Old Generation에 대해 **[mark-sweep-compact](https://plumbr.io/handbook/garbage-collection-algorithms/removing-unused-objects/compact)를 사용.** 이름에서 알 수 있듯이 이 수집기 둘 다 단일 스레드 수집기이므로 작업을 병렬화할 수 없습니다.
-   Stop the world 시간이 길다.
-   싱글 쓰레드 환경 및 heap이 매우 작을 때 사용한다.

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F06f3c788-a8f0-412c-93f7-6d43ad017121%2FUntitled.png?id=41ae7f6a-6a34-447e-8551-9d3b7e678888&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1920&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)


### 방식2 : Parallel GC

-   여러 개의 쓰레드로 GC실행
-   Young Generation  에서는 **[mark-copy](https://plumbr.io/handbook/garbage-collection-algorithms/removing-unused-objects/copy)** 를 사용  하고 Old Generation에서는 **[mark-sweep-compact 를 사용](https://plumbr.io/handbook/garbage-collection-algorithms/removing-unused-objects/compact).**
-   Young 및 Old 컬렉션은 모두 stop-the-world 이벤트를 트리거하여 가비지 수집을 수행하기 위해 모든 애플리케이션 스레드를 중지.
    -   모든 코어가 가비지를 병렬로 청소하므로 일시 중지 시간이 짧아진다.
    -   가비지 콜렉션 주기 사이에 수집기 중 어느 것도 리소스를 소비하지 않는다.
-   멀티코어 환경에서 사용
-   Java 8의 default GC 방식

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F201d552d-5e17-4479-8036-bd3d060de7d1%2FUntitled.png?id=74bddabb-260e-4906-b6fc-fb59243b84c7&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1920&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)


### [방식3 : CMS GC](https://plumbr.io/handbook/garbage-collection-algorithms-implementations#concurrent-mark-and-sweep)

-   Stop The World 최소화를 위해 고안
-   GC 작업을 어플리케이션과 동시에 실행
-   G1 GC등장에 따라 대체 되었다.

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F04eb2d40-c2a8-48b4-b527-b3a2fd2d750b%2FUntitled.png?id=382ffe91-9635-40c8-9a36-9414d4428c11&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1920&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

-   단점
    -   메모리와 CPU를 많이 사용하고
    -   `Compaction`이 기본 제공되지 않는다.

### 방식4 : G1 GC

-   Garbage First(G1)
-   Heap을 Region으로 나누어 사용
-   Java9 부터 default GC 방식

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F1a39a2a3-f5eb-47a4-badb-62ef2f4b895c%2FUntitled.png?id=bbd0cb8d-b967-495f-a667-22b16cb0cf35&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1920&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

-   G1 GC가 필요에 따라 영역별 Region 개수를 튜닝한다.
-   Stop the world를 최소화 할 수 있다.

## JVM GC 튜닝

-   성능 개선의 최종 단계라고 봐야한다.
    -   객체 생성 자체를 줄이려는 코드 개선이 선행되어야 한다.
    -   예시 : StringBuilder 사용 등
-   목표
    -   Old Generation 으로 넘어가는 객체 최소화하기. (Major GC 적게 발생시키기)
    -   Major GC 시간을 짧게 유지하기
-   튜닝 과정
    1.  GC 상태 모니터링
    2.  알맞은 GC 방식과 메모리 크기 설정
        1.  너무 크다고 좋지 않다. 적게 실행되지만 오래 걸린다.
    3.  적용하기

### JVM 모니터링 방법 : jstat

-   명령어를 사용해 GC를 모니터링 할 수 있다.
    
-   사용 시간, 횟수
    
    ![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F3e2af9db-3b7a-4fe6-ab3f-c7fc895afc30%2FUntitled.png?id=b00cb1fb-bd3d-4f2b-bc1b-3beb9d0aa3ec&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1920&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)
    
-   영역 사용률
    
    ![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F0af7c983-ef83-4199-92e1-0428cd842195%2FUntitled.png?id=3e28bf8e-c97c-449f-8a2e-aabad64981d9&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=1920&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)
    

### 튜닝시 옵션

-   GC 튜닝 시 기본적으로 확인인해야 하는 JVM 옵션
| 구분 | 옵션 | 설명 |
| --- | --- | --- |
| 힙(heap) 영역 크기 | -Xms | JVM 시작 시 힙 영역 크기 |
|  | -Xmx | 최대 힙 영역 크기 |
| New 영역의 크기 | -XX:NewRatio | New영역과 Old 영역의 비율 |
|  | -XX:NewSize | New영역의 크기 |
|  | -XX:SurvivorRatio | Eden 영역과 Survivor 영역의 비율 |
- GC 방식에 따라 지정 가능한 옵션

| 구분 | 옵션 | 비고 |
| --- | --- | --- |
| Serial GC | -XX:+UseSerialGC |  |
| Parallel GC | -XX:+UseParallelGC-XX:ParallelGCThreads=value |  |
| Parallel Compacting GC | -XX:+UseParallelOldGC |  |
| CMS GC | -XX:+UseConcMarkSweepGC-XX:+UseParNewGC-XX:+CMSParallelRemarkEnabled-XX:CMSInitiatingOccupancyFraction=value-XX:+UseCMSInitiatingOccupancyOnly |  |
| G1 | -XX:+UnlockExperimentalVMOptions-XX:+UseG1GC | JDK 6에서는 두 옵션을 반드시 같이 사용해야 함 |



[NAVER D2](https://d2.naver.com/helloworld/37111)

[GC Tuning: Basics | Plumbr - User Experience & Application Performance Monitoring](https://plumbr.io/handbook/gc-tuning)

---

-   참고
    -   [](https://plumbr.io/handbook/what-is-garbage-collection)[https://plumbr.io/handbook/what-is-garbage-collection/automated-memory-management/reference-counting](https://plumbr.io/handbook/what-is-garbage-collection/automated-memory-management/reference-counting)
    -   [](https://d2.naver.com/helloworld/37111)[https://d2.naver.com/helloworld/37111](https://d2.naver.com/helloworld/37111)
    -   [](https://youtu.be/vZRmCbl871I)[https://youtu.be/vZRmCbl871I](https://youtu.be/vZRmCbl871I)