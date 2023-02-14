## **연속 할당 방식**

### **고정분할 방식 Fixed partition allocation**

-   물리적 메모리를 몇 개의 영구적 분할로 나눕니다.
-   분할의 크기가 모두 동일한 방식도 있고 서로 다른 방식도 있습니다.
-   분할 하나의 공간에 하나의 프로그램을 적재합니다.
-   융통성이 없습니다.
    -   동시에 메모리에 load되는 프로그램의 총 수가 제한됩니다.
    -   최대 수행 가능한 프로그램의 크기도 제한됩니다.
-   Internal fragmentation 이나 External fragmentation이 발생할 수 있습니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F1SZ6I%2FbtrZc7ltKtW%2FGQxgSjnCfMs80yRd6n5vdk%2Fimg.png)
> **😗 외부 조각과 내부 조각은 무엇일까?  
> 외부 조각 External fragmentation**  
> \- 프로그램 크기보다 분할의 크기가 작은 경우  
> \- 아무 프로그램에도 배정되지 않은 빈 곳이지만, 프로그램이 올라갈 수 없는 작은 분할을 뜻한다.  
>   
> **내부 조각 Internal fragmentation**  
> \- 프로그램 크기보다 분할의 크기가 큰 경우  
> \- 하나의 분할 내부에서 발생한다. 특정 프로그램에 배정되어 있지만 사용되지 않는 공간을 뜻한다.

### **가변분할 방식 Variable partition allocation**

-   처음 실행 시에 낮은 메모리에서부터 차곡차곡 실행합니다.
-   프로그램의 크기를 고려하여 할당합니다.
-   분할의 크기, 개수가 동적으로 변할 수 있습니다.
-   기술적 관리 기법이 필요합니다.
-   External fragmentation이 발생할 수 있습니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbpf6Sy%2FbtrZbPevxBa%2FffOA6wTkN6w88dkLs5aOs0%2Fimg.png)

-   예시
    -   만약 프로그램 일부가 끝난다면 그대로 빈 공간이 됩니다.
    -   새로 실행하는 프로그램이 이 빈 공간에 들어갈 수 없다면 더 높은 메모리에 위치하게 됩니다.

#### **🕳️ Hole 이 생깁니다.**

-   Hole 은 가용 메모리 공간입니다.
-   다양한 크기의 hole 들이 메모리 여러 곳에 흩어져 있습니다.
-   실행할 프로세스가 도착하면 수용 가능한 hole 을 할당합니다.
-   운영체제는 **할당 공간**과 **가용 공간**(hole)의 정보를 유지하고 있습니다.
    -   프로그램이 실행될 때 그럼 어디로 넣어야 할 지 정해야 하는 문제가 생깁니다. 👉 **Dynamic Storage-Allocation Problem**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fky3lX%2FbtrY4njhLKX%2Fp7BNfhtXxRMhLLAidLxeE0%2Fimg.png)

#### ****동적 스토리지 할당 문제 Dynamic Storage-Allocation Problem****

> 가변 분할 방식에서 size n 인 프로세스의 요청을 만족하는 가장 적잘한 hole을 찾는 문제  
> 메모리 공간 효율을 위해 고려합니다.

1.  **First-fit**
    -   크기가 n 이상인 hole 중 최초로 찾아지는 hole에 할당합니다.
2.  **Best-fit**
    -   크기가 n 이상인 hole 중 가장 작은 hole을 찾아서 할당합니다.
    -   hole 리스트가 크기순으로 정렬되지 않은 경우 모든 hole의 리스트를 탐색해야 합니다.
    -   많은 수의 아주 작은 hole 들이 생성됩니다.
3.  **Worst-fit**
    -   가장 큰 hole 에 할당하는 규칙입니다.
    -   모든 hole을 탐색해야 알 수 있습니다.
    -   상대적으로 아주 큰 hole 들이 생성됩니다.

> **First-fit** 과 **Best-fit** 이 worst-fit 보다 속도와 공간 이용률 측면에서 효과적입니다.

#### **메모리 압축 compaction**

> External fragmentation 을 해결하는 한 가지 방법입니다.  
> 작은 hole 이 너무 많아졌을 때는 사용중인 메모리를 한 곳으로 몹니다. (디스크 조각모음과 비슷합니다.)

-   hole 들을 한 곳으로 몰아 큰 block을 만드는 것입니다.
-   매우 비용이 많이 듭니다.
-   최소한의 메모리 이동으로 Compaction을 하는 방법은 매우 복잡한 문제이기 때문에 어떤 메모리가 이동할 것인가 선택하는 것도 어렵습니다.
-   Compaction은 프로세스 주소가 실행 시간에 동적으로 재배치가 가능한 경우에만 수행 가능합니다.