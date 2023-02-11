## **메모리 주소**

-   프로그램을 실행시키면 그 데이터가 메인메모리를 차지하면서 실행됩니다.
    -   정확히는 디스크 스케줄링에 의해 어떤 프로세스가 수행될 지 결정되고 그 결정된 프로세스가 메모리 레디큐에 올라가는 것입니다.
-   메모리 각 저장공간에는 **주소**가 매겨져 있습니다. OS나 프로그램은 메모리에 주소를 통해서 접근할 수 있습니다.
-   주소는 **논리적 주소**와 **물리적 주소** 두 가지로 나누어 생각할 수 있습니다.

### **논리적 주소 `Logical address`**

-   `virtual address` 라고도 합니다.
-   프로세스마다 독립적으로 가지는 주소 공간을 뜻합니다.
-   각 프로세스마다 **0**부터 시작합니다.
-   CPU가 보는 주소이기도 합니다.

### **물리적 주소 `Physical Address`**

-   메모리에 실제 올라가는 주소를 뜻합니다.
-   물리적인 메모리는 하나로 0부터 통째로 관리됩니다.
-   0에는 커널이 올라가 있고, 그 상위 주소는 여러 프로그램들이 나누어 사용합니다.

### **상징적 주소 `Symbolic Address`**

-   프로그래머가 프로그래밍을 할 때, 변수 이름이나 메소드 이름으로 메모리에 접근을 합니다. 이를 Symbolic Address라고 합니다.
-   이 것이 컴파일 되면 숫자로 된 논리적 주소로 바뀝니다. 그리고 이를 실행하기 위해서 물리적 주소로 바뀌게 됩니다.

-   예시로 다음과 같은 코드가 있다고 합시다. 

```
Data data = 10;
```

1.  `data`라는 번지에다 10을 저장하는 코드입니다.
2.  실제로 CPU가 명령어를 수행하면 다음과 같이 수행합니다.
3.  `store #0x00198000, 10 // data가 0x00198000에 위치해있고, 10을 저장한다는 뜻입니다.`

-   그럼 `data`가 저장될 `0x00198000`은 언제 결정될까요? 👀
    -   주소 바인딩 Address binding에 대해 알아봅시다.

---

## **주소 바인딩**

-   주소 변환이라고도 합니다.
-   어떤 프로그램이 **물리적인 메모리 어디로 올라갈 지 결정하는 것**을 주소 바인딩이라고 합니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbicdgk%2FbtrYjlkDD7Y%2Fp1FQFM9kYnKdyjkpdIe8FK%2Fimg.png)

-   주소를 결정하는 방법은 3가지가 있습니다.  
    -   **Compile time binding** : 프로그램 로딩 전
    -   **Load time binding** : 프로그램 로딩 시
    -   **Run time binding** : 프로그램을 실행하며

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbJET21%2FbtrX7YR8Upr%2Fw4tOc5wLsWIU5HSlgSxl30%2Fimg.png)

---

### **Compile time binding**

-   프로그램을 메모리에 로드하기 전에 수행됩니다.
-   물리적 메모리 주소 `physical address`가 컴파일시 알 수 있습니다.
    -   컴파일 타임에 결정되는 메모리 할당
-   시작 위치를 변경하면 재컴파일 합니다.
-   컴파일러는 절대코드 `absolute code`를 생성합니다.

#### **✋ absolute code란?**

-   어셈블리어가 정한 위치에 **물리적으로 고정되어 있는 코드**
-   relocatable code의 반댓말

#### **정말 가능한 방법일까?**

-   사실 이 방법은 요즘 잘 사용하지 않습니다. 프로그램이 메모리에서 주소를 지정해도, 실제로 이 메모리에 이미 다른 프로세스가 있다면? 안되겠죠.
-   사실상 이 방식이 사용되는 방식은 단 하나, 아무것도 없을 때입니다.
    -   OS도 없고 프로세스도 딱 하나뿐인 상황, 즉 **임베디드 시스템**에서 사용합니다.

---

### **Load time binding**

-   Loader의 책임하에 물리적 메모리 주소를 부여합니다.
    -   즉 Loading할 때 결정되며, 프로그램 내부 주소와 물리적 주소가 다릅니다. 프로그램 내부의 메모리 시작을 0번지부터 다시 매깁니다.
    -   compile time : 프로그램 내부 주소 == 물리적 주소
-   컴파일러가 재배치가능코드 `relocatable code`를 생성한 경우 가능합니다.

#### **로드 타임 바인딩 시 주소 할당 문제**

-   실제로 로딩타임에 메모리주소를 결정하는 방법은 잘 사용되지 않습니다.
-   로딩할 때마다 모든 메모리주소가 한 번씩 다 바뀌어야 하기 때문에 계산이 오래걸려 **메모리 로딩에 시간이 매우 오래걸립니다.**

#### **Excution time binding (=Run time binding)**

-   프로그램을 메모리 로드한 후에도 주소 바인딩을 연기합니다.
    -   수행이 시작된 이후에도 프로세스 메모리상 위치를 옮길 수 있습니다.
    -   프로그램이 실행될 때까지 메모리의 위치를 계속해서 변경하게 됩니다.
-   CPU가 주소를 참조할 때마다 binding을 점검합니다.
-   프로그램 실행시 프로세서에 의해 수행됩니다.
-   주소를 매번 변환시켜서 주소를 얻는 변환용 하드웨어 지원이 필요합니다. 바로 MMU(Memory management unit) 입니다.

#### **주소변환을 위한 하드웨어 MMU**

-   **Memory Management Unit**
    -   logical address 를 physical address로 매핑해주는 Hardware device
-   **MMU scheme**
    -   사용자 프로세스가 CPU에서 수행되며 생성해내는 모든 주소값에 대해 `base register`의 값을 더한다.
-   **user program**
    -   logical address만을 다룹니다.
    -   실제 physical address를 볼 수 없으며 알 필요가 없습니다.

#### **아주 간단한 주소 변환의 예시 MMU scheme**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbq7jNX%2FbtrYdihhMmB%2FJO1HyjaYZkc5yKKpJIDCJ0%2Fimg.png)

-   그림의 흐름
    1.  CPU가 논리적 주소 346을 요청합니다.
    2.  주소 변환이 필요한데, 가장 간단한 주소 변환은 Relocation register(==base register)와 limit register 로 이루어집니다.
    3.  시작위치인 relocation register 와 가상 메모리 주소를 더하면 됩니다. 그림에서는 `14000 + 346 = 14346`으로 계산되어 물리적 주소 14346으로 찾아가게 됩니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbAtExi%2FbtrX31VRGa6%2F9G2kVuEuB83f6tM2VEeFX0%2Fimg.png)

-   다른 방법으로는 limit register를 이용합니다.
    1.  만약 가상 메모리 주소가 잘못되어 4000번지를 요청하게 되면, 엉뚱한 물리적 주소를 찾아가게 됩니다.
    2.  이런 경우에는 악의적인 프로그램이기 때문에 이를 막아야 합니다.
    3.  그래서 요청이 들어오면 논리 주소가 유효한가 limit register와 요청된 logical address를 비교합니다.

### **컴파일 타임 주소바인딩과 로드 타임 주소바인딩의 차이점**

| **Compile time 주소 바인딩** | **Load time 주소 바인딩** | **Run time 주소 바인딩** |
| --- | --- | --- |
| 컴파일러는 컴파일 시간 주소 바인딩을 담당합니다. | 로더는 로드 시간 주소 바인딩을 담당합니다. | 실행 시간 주소 바인딩은 프로세서에 의해 수행됩니다. |
| 논리 주소(가상 주소)를 생성합니다. | 물리적 주소를 생성합니다. | 동적 절대 주소를 생성합니다. |
| 프로그램을 메모리에 로드하기 전에 수행됩니다. | 프로그램을 메모리에 로드한 후에 완료됩니다. | 프로그램 실행 시 수행됩니다. |
| 정적 주소 바인딩입니다. | 또한 정적 주소 바인딩이지만 일부 운영 체제에서는 동적 주소 바인딩을 지원합니다. | 동적 주소 바인딩입니다. |
| 컴파일러는 이를 수행하기 위해 운영 체제 메모리 관리자와 상호 작용합니다. | 운영 체제 메모리 관리자 자체에서 수행합니다. | 프로그램 실행 시 프로세서에 의해 수행됩니다. |

-   출처 : [https://www.geeksforgeeks.org/difference-between-compile-time-and-load-time-address-binding/](https://www.geeksforgeeks.org/difference-between-compile-time-and-load-time-address-binding/)

## **ref.**

-   [반효경 운영체제 Memory Management](http://www.kocw.net/home/search/kemView.do?kemId=1046323)
-   [양햄찌가 만드는 세상](https://jhnyang.tistory.com/133)