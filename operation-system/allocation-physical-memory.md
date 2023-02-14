## **메모리의 두 영역**

-   OS 상주 영역
    -   낮은 주소 영역
    -   인터럽트 벡터`interrupt vector` 와 함께 사용
-   사용자 프로세스 영역
    -   높은 주소 영역

## **사용자 프로세스 영역의 할당 방법**

### **[연속 할당 Contiguous allocation](./contiguous-allocation.md)**

> 각 프로세스가 메모리의 연속적인 공간에 적재되는 방법

-   고정분할 방식 Fixed partition allocation
-   가변분할 방식 Variable partition allocation

### **불연속 할당 Noncontiguous allocation**

> 하나의 프로세스가 메모리 여러 영역에 분산되어 적재되는 방법  
> 현대 시스템에서 사용한다.

-   **[Paging](./paging.md)** ⭐️
-   Segmentation
-   Paged Segmentation