## **세그먼테이션 Segmentation**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FrwwgS%2FbtrZ2zio8BG%2FO719dI5wtnPPK7bwDkKVI0%2Fimg.png)

> 불연속 할당 방식의 하나  
> 세그먼테이션은 페이징과 달리 프로세스를 물리적 단위인 페이지가 아닌 논리적 단위인 세그먼트로 분할해서 메모리에 적재하는 방식을 말한다.

-   분할 방식을 제외하면, 페이징과 세그멘테이션이 동일하기 때문에 매핑 테이블의 동작 방식도 동일하다.
    -   가변 분할 다중 프로그래밍에서 이용된 방법과 동일하게 배치되며
    -   일반적으로 **최초적합First-fit**과 **최적적합Best-fit**이 이용된다.
-   세그멘테이션은 프로세스를 **논리적 내용을 기반으로 나눠서** 메모리에 배치하는 것을 의미한다.
-   참고하고자 하는 세그먼트가 주 기억장치에 있으면 프로세스에 의해 계속 실행되며, 현재 주 기억장치에 없으면 보조기억장치로부터 주기억장치로 옮겨온다. 주기억장치에 옮겨지는 세그먼트가 들어갈 만큼의 충분한 공간이 연속적으로 확보되어야 한다.

### **세그먼트 segment**

-   가상 메모리를 서로 크기가 다른 논리적 단위로 분할한 것을 의미한다.
-   논리적 단위가 되는 프로그램 모듈, 자료구조 등
-   고유한 이름과 길이를 가진다.
-   <segment, offset> 형태로 구성되며, 세그먼트 번호를 통해 세그먼트의 기준 (세그먼트의 시작 물리 주소)와 한계 (세그먼트의 길이)를 파악할 수 있다.

```
세그먼트 번호 S , 변위 d

가상주소 v = (s,d)
```

-   세그먼트는 특정 크기를 갖도록 제안받지 않는다.
    -   배열에 대응되는 세그먼트의 크기 == 배열의 크기
    -   동적 자료구조에 대응되는 세그먼트의 크기 == 자료구조가 가지는 크기

### **순수 세그먼테이션 시스템에서 가상 주소 변환**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqOiM3%2FbtrZ67L8Ard%2Fh8cCgw9jKotzB4oIjGQnCk%2Fimg.png)

### **세그먼트 사상 테이블 항목**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FWCqpg%2FbtrZUBOAGM2%2F3TIq9xkTk7CLgerPxWn2V1%2Fimg.png)

-   **세그먼트 부재 결함 segment missing fault**
    -   발생원인 : 존재 비트 r을 점검하여 만약 없으면 세그먼트 부재 결함을 발생
    -   대처 : 운영체제가 보조기억장치 주소 a로부터 세그먼트를 적재시킨다.
-   세그먼트 오브플로우 결함 segment overflow fault
    -   발생 원인 : 세그먼트가 적재되면 변위d가 세그먼트 길이L보다 작거나 같은지 점검하면서 주소 변환하다 d가 L보다 크면 세그먼트 오버플로우 결함 발생
    -   대처 : 운영체제가 그 프로세스에 대한 처리를 종결시킨다.

### **세그먼트의 논리 단위**

> 프로세스를 code 영역, data 영역, stack 영역 등으로 나누는 것 또한 세그먼테이션이라고 할 수 있다.

-   main program
-   procedure
-   function
-   method
-   object
-   stack
-   local variable
-   global variable
-   etc...

### **세그먼트의 공유와 보호**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbioDob%2FbtrZ6iHb8fF%2FufnaRLAOO4r5QxhiJazp60%2Fimg.png)

-   페이징 기법과 비슷하다.

---

## 페이징과 세그먼테이션의 차이점은?

> 외부단편화, 내부단편화와 함께 반드시 미리 정리해두자. [단편화 복습](https://new-pow.tistory.com/32)

-   **페이징** : 프로그램을 같은 **일정 크기**의 페이지로 분할. 외부 단편화를 해결할 수 있지만, 내부단편화가 발생한다.
-   **세그멘테이션** : 논리적 의미를 기준으로 **필요한 크기만큼** 세그먼트를 분할. 프로세스 크기만큼 할당하므로 내부 단편화는 생기지 않는다. 다만 외부 단편화가 발생한다.

세그먼테이션은 페이징보다 보호와 공유 면에서 더 좋은 방법이다.

 **세그먼테이션**은 code, data, stack을 논리적으로 나누기 때문에 비트를 설정하기 간단하고 안전하다. 반면 페이징은 각 영역을 무시하고 일정한 크기로 나누기 때문에 영역이 섞여 비트 설정에 까다로워질 수 있다.

 공유할 때도 페이징은 순서가 섞일 가능성이 존재한다.

하지만 현재 대부분 페이징 기법을 주로 사용하는데, 그 이유는 세그먼트가 다양한 hole이 발생하는 외부단편화가 있기 때문에 메모리 낭비가 크기 때문이다.

---

-   [운영체제 가상 메모리 관리-세그멘테이션](https://youtu.be/lmeVVVapQUQ)  
-   [운영체제 - 메모리 단편화](https://youtu.be/zjFpWi_tqDo)