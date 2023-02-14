## **페이징 Paging**

> **불연속 할당 방식**의 하나  
> 프로그램을 구성하는 가상 주소 공간을 같은 크기의 페이지로 분할합니다. 페이지 단위로 물리적인 메모리에 올려두거나 Backing storege에 내려놓거나 합니다.

-   물리적인 메모리의 공간을 `페이징 프레임 paging frame`이라고 부릅니다.
-   균일한 크기로 잘려있기 때문에 hole의 크기가 각각 달라서 생기는 문제점은 없습니다.
-   반면 **주소 변환은 굉장히 복잡해 집니다.** 더이상 하나의 프로세스가 연속된 주소를 가진다는 보장이 없기 때문입니다.

## **페이징의 메소드**

-   물리적 메모리를 동일한 크기의 `frame`으로 나눕니다.
-   논리적 메모리를 동일한 크기의 `page`로 나눕니다. 이 때, **`frame`과 `page`의 크기는 같습니다.**
-   모든 가용 frame들을 관리합니다.
-   `page table`을 사용하여 논리 주소를 물리 주소로 변환합니다.
-   외부 단편화 `External fragmentation`은 발생하지 않으나 내부 단편화`Internal fragmentation`은 발생할 수 있습니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FVW9dJ%2FbtrZjqTnE3H%2FunSJ8bVAXPLGhfYa42ula1%2Fimg.png)

## **페이지 테이블 Page table**

-   프로세스의 페이지가 어떤 식으로 프레임에 mapping 되는지 알 수 있습니다.
-   페이지 테이블은 모든 프로세스마다 개별적으로 가지고 있는 정보입니다.
-   페이지 테이블은 용량이 꽤 크고 (대부분 인덱스마다 4KB) 메모리 정보를 가지고 있으므로 자주 봐야하기 때문에 커널(메인 메모리)에 저장되어 있습니다.
-   `Page-table base register (PTBR)` 이 page table을 가르킵니다.
-   `Page-table length register (PTLR)` 이 page table의 길이를 보관합니다.
-   모든 메모리 접근 연산에는 2번의 메모리 접근이 필요합니다.
    -   page tagle 접근 1번
    -   실제 data/instruction 접근 1번
-   속도 향상을 위해 별도의 하드웨어 구조
    -   `associative register` 혹은 가상 `translation look-aside buffer (TLB)` 라는 고속의 lookup hardware cache를 사용합니다.
-   단점
    -   모든 프로세스 별로 그 logical address에 대해 대응하는 모든 page에 엔트리가 존재합니다.
    -   대응하는 page가 메모리에 있든 아니든 간에 page table에는 엔트리가 있으니 사이즈가 매우 큽니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdxNcbU%2FbtrZchvN0Lq%2Fwl7klPiE11nJoMAIkfgFkk%2Fimg.png)

### **Translation look-aside buffer TLB란?**

자주 참조되는 가상 메모리 주소를 실제 메모리 주소로 매핑 시 성능 개선 위해 MMU에서 사용하는 고속 캐시  
빈번하게 사용되는 페이지 정보를 가지고 있습니다. CPU가 page table에 접근하기 전에 먼저 TLB를 탐색합니다.  
[참고링크](http://blog.skby.net/tlb-translation-look-aside-buffer/)

주의할 것은 일부만 저장한다는 것입니다. 논리적인 페이지번호 p와 프레임 번호 f를 가지고 있습니다.  
또 다른 주의사항은 TLB를 매번 전체를 서치하며 찾아보아야 한다는 것입니다. (page table에서는 p번째에 바로 접근하면 됩니다.)  
이 때문에 `Associative register` 를 이용하여 병렬 검색이 가능하도록 했습니다.

TLB는 문맥 교환 때 flush 되어 오래된 엔트리가 삭제됩니다. 프로세스마다 메모리 접근 주소가 다르기 때문입니다.

### **2단계 페이지 테이블 Two-Level Page Table**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbvtIz6%2FbtrZc61XmhE%2FyDamdlYMWSlkkS3NjA5Ynk%2Fimg.png)

> 👀 왜 이걸 쓸까요?

-   속도는 줄어들지 않습니다. 그러나 page table을 위한 저장 공간이 줄어듭니다.
-   1단계 페이징의 경우 중간에 빈 공간이 없이 index를 모두 다 사용해야 합니다.
-   2단계 페이징의 경우 페이지 번호 주소체계를 하나 더 둡니다. page table 자체가 page로 구성되었습니다.
    -   안쪽 페이지 테이블의 경우 상당부분 사용이 안되는 부분은 null 이다.  
        ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FT81Tx%2FbtrZjzIEptY%2FQCndOl7pYpJa0nHzTLVl50%2Fimg.png)

[참고링크](https://charles098.tistory.com/108)

### **다단계 페이지 테이블 Multilevel Paging and Performance**

-   Address space가 더 커지면 다단계 페이지 테이블이 필요합니다.
-   각 단계의 페이지 테이블이 메모리에 존재하므로 logical address의 physical address 변환에 더 많은 메모리 접근이 필요합니다.
-   TLB를 통해 메모리 접근 시간을 줄일 수 있습니다.

[참고링크](https://sonsh0824.tistory.com/entry/MultiLevel-Page-Table)

### **Vaild-Invalid Bit in a Page Table**

-   Page table의 각 엔트리 마다 이런 bit를 둡니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FBxGD8%2FbtrZddU8Qoh%2FKKTaUdSnAqO1qzuku1jDPK%2Fimg.png)

1.  **Protction bit**
    -   page에 대한 접근 권한 (read / write / read-only)
    -   어떤 연산에 대한 접근 권한이 있는가를 나타냅니다.
2.  Valid-invalid bit
    -   `valid` 해당 주소의 frame에 그 프로세스를 구성하는 유효한 내용이 있음을 뜻합니다. 접근 허용
    -   `invalid` 해당 주소의 frame에 유효한 내용이 없음을 뜻합니다. 접근 불허
        -   프로세스가 그 주소 부분을 사용하지 않는 경우 null
        -   해당 페이지가 메모리에 올라와 있지 않고 swap area에 있는 경우

### **Page 👉 Frame Mapping 과정**

1.  오프셋 Offset
    -   위치를 찾기 위해 더해주는 값입니다.
    -   `현재 주소 = (#페이지 * 페이지크기) + offset`

![](https://odinuv.cz/common/pagination/offset-limit.svg)

|   | page 1 | page 2 | page 3 | page 4 | page 5 |
| --- | --- | --- | --- | --- | --- |
| LIMIT | 25 | 25 | 25 | 25 | 25 |
| OFFSET | 0 | 25 | 50 | 75 | 100 |
| results | 0–24 | 25–49 | 50–74 | 75–99 | 100–104 |

2.  페이지 테이블 Page Table
    -   구체적으로 각 페이지에 **물리적 주소에서의 시작 주소값 base address** 이 저장되어 있습니다.
    -   `인덱스 - 값`의 자료 구조를 가집니다.
    -   페이지의 개수만큼 페이지 테이블의 인덱스가 있습니다.

```
base address + offset = physical address
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDDjtG%2FbtrZeinn3vQ%2FL9aZOG3UHejCJuM1F9ZOMK%2Fimg.png)

## **Inverted Page Table**

-   Page frame 하나당 page table 하나의 엔트리를 둔 것 (system-wide)입니다. 완전히 역발상이지요.
-   각 page table entry는 각각의 **물리적 메모리 page frame**이 담고 있는 내용을 표시합니다.
-   페이지 프레임 f번째 엔트리 -> 논리 주소 위치
-   **테이블 전체를 탐색해야 하는 단점**이 있기 때문에 `associative register`를 사용합니다.
-   저장 공간을 아낄 수 있다는 장점이 있습니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc2XNSV%2FbtrZiWryL5n%2FxnxVcaeayt0t1FSfpLfgiK%2Fimg.png)

## **Shared Pages**

-   여러 프로세스에 의해 공통으로 사용될 수 있도록 작성된 코드를 말합니다.
-   재진입 가능 코드 혹은 순수 코드라고도 불립니다.
-   조건
    -   읽기 전용 `read only` 여야 합니다.
    -   동일한 물리적 메모리 주소를 가지고 있어야 합니다.
    -   모든 프로세스의 논리적 주소 공간에서 동일한 위치에 존재해야 합니다.
-   물리적 메모리에는 하나씩의 코드만 올라갑니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbot2jN%2FbtrZjyRe9TJ%2FkXKWykDAwMr7yJ7yx62R1K%2Fimg.png)