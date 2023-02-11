> 메모리 관리 용어를 먼저 정리해봅시다.

## **동적 적재 Dynamic Loading**

-   프로세스 전체를 메모리에 미리 다 올리는 것이 아니라 **해당 루틴이 불려질 때 메모리에 load** 하는 것을 뜻합니다.
-   메모리 효용성이 향상됩니다.
-   가끔씩 사용되는 많은 양의 코드의 경우 유용하게 사용됩니다.
    -   모든 코드가 자주 사용되지는 않습니다. 예를 들어 **오류 처리 루틴**의 경우 미리 통째로 메모리에 올려놓는 것은 비효율적입니다.
-   원래 Dynamic Loading이라는 말은 운영체제의 **특별한 지원 없이 프로그램 자체에서 구현**하는 것을 뜻합니다.
    -   OS의 경우 라이브러리를 통해 지원 가능하므로 일일히 개발자가 만들지는 않습니다.
    -   페이징과 다른 말이지만, 최근은 페이징과 섞어쓰기도 합니다.

---

## **오버레이 Overlays**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdUllaK%2FbtrYfZJ4Ptt%2F73L1wgMAVeUPCA0TWOKdI1%2Fimg.png)

-   메모리에 실제 필요한 정보만을 load합니다.
-   프로세스 크기가 메모리보다 클 때 유용합니다.
-   운영체제의 지원없이 사용자에 의해 구현합니다.
-   현재는 VMM (Virtual memory management)가 나온 이후 필요없는 기법이 되었지만, 한 때 유용하게 쓰였습니다.
-    overlay driver : 이 기법을 쓰기 위해 필요한 상대적으로 작은 메모리를 차지하는 드라이버. 상황에 맞춰 메모리를 올렸다 내렸다 하는 중재자 역할을 수행해줍니다. 
-   Dynamic Loading과 굉장히 비슷해보이지만 역사적으로 Dynamic Loading과 다릅니다.
    -   작은 공간의 메모리를 사용하던 초창기 시서템에서 수작업으로 프로그래머가 구현해왔습니다.
    -   그래서 Manual Overlay라고도 합니다.
    -   하나하나 직접 구현했기 때문에 프로그래밍이 매우 복잡합니다.

---

## **스와핑 Swapping**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fba6OjQ%2FbtrYjfehO6K%2FTRIrcqgHY82kP8G6xcYGI1%2Fimg.png)

-   **프로세스를 메모리에서 하드디스크의 Backing store로 통째로 쫓아내는 것** 입니다.
-   최근에는 페이징에서 한 페이징이 쫓겨날 때 swap out되었다고 표현도하지만 원래는 통째로 쫓겨난다는 뜻을 가지고 있습니다.
    -   **Swap Out**: 주기억장치에 있는 프로그램이 보조기억장치로 이동
    -   **Swap In**: 보조기억장치에 있는 프로그램이 주기억장치로 이동
-   가상기억장치의 페이징 기법으로 발전하였습니다.

-   일반적으로 중기 스케줄러 swapper에 의해 swap out 시킬 프로세스를 선정합니다.
    -   priority-based CPU scheduling algorithm 에 의해 결정됩니다. 우선순위가 낮다면 swqp out 시키고, 우선순위가 높다면 다시 메모리에 올려놓는 것이지요.

### **swap in 을 할 때의 규칙**

-   Compile time / Load time binding 에서는 원래 메모리 위치로 swap in 합니다. 스와핑의 효과를 활용하기 어렵습니다.
-   Execution time binding 에서는 빈 메모리 영역 아무데나 올릴 수 있습니다.
    -   300번지에 있던 메모리가 쫓겨났다가 다시 돌아오면 어디든 들어갈 수 있으므로 더 효율적입니다.

### **스와핑의 장점과 단점**

-   하드디스크에 있던 것을 다시 메모리에 로딩시켜야 하니 좀 느립니다.
    -   swap time은 대부분 transfer time(데이터를 전송하는 시간) 으로 swap 양에 비례하는 시간이 걸립니다.
-   하지만 부족한 메모리에 더 많은 프로세스를 실행할 수 있습니다.
    -   메모리 효율성 면에서 좋습니다.

---

## **Dynamic Linking**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FRfV0j%2FbtrX9Gc9GyE%2FsQjneonAZ47Yxtu8ii4vFk%2Fimg.png)

### **Linking이란?**

-   Link는 여러 곳에 존재하던 컴파일 된 파일들을 묶어 하나의 실행파일로 만드는 것을 뜻합니다.
    -   내가 작성한 함수들 + 유용한 라이브러리 ... = 실행파일
-   Linking을 실행 시간(execution time)까지 미루는 기법입니다.

### **Static Linking**

-   라이브러리가 프로그램의 실행 파일 코드에 포함됩니다.
-   실행 파일의 크기가 큽니다.
-   동일한 라이브러리를 각각의 프로세스가 메모리에 올리므로 메모리가 낭비됩니다.
    -   예를 들어 printf코드를 100개의 프로그램이 각각 직접 가지고 있다면? 메모리가 더 필요하겠죠.

### **Dynamic Linking**

-   라이브러리가 실행시에 연결됩니다.
-   라이브러리가 별도의 파일로 존재하고, 라이브러리에서의 위치를 찾을 수 있는 소위 포인터인 stub만 실행 파일코드에 포함해 놓습니다.
-   혹은 메모리에 이미있으면 그 루틴의 주소로 가고 없으면 디스크에서 별도의 파일로부터 라이브러리를 찾아서 필요하면 메모리에 올립니다.
    -   예를 들어 printf코드를 disk에 있고 100개의 프로그램이 이 코드의 주소를 가지고 있다면?
    -   이런 이미 가지고 있는 라이브러리를 shared library라고 합니다.
-   운영체제의 도움이 필요합니다.

## **ref.**

-   [반효경 운영체제 : 메모리 관리](http://www.kocw.net/home/search/kemView.do?kemId=1046323)
-   [양햄찌가 만드는 세상](https://jhnyang.tistory.com/42)