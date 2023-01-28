# 프로세스 Process
> Process is a program in excution  
> 프로세스는 실행중인 프로그램이다. 작업Job, 테스크Task라고도 한다.


![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbbrOsK%2FbtrW4Ee0uLT%2FkL6oZ81Vv425T7PKlJUHKk%2Fimg.png)

메모리에 적재되어 실행되고 있는 프로그램.
프로그램이 명령어 리스트를 가지고 디스크에 저장되어 있는 정적파일이라면, 프로세스는 이 프로그램이 실행중인 작업을 의미한다. 따라서 하나의 프로그램으로 여러 프로세스를 띄울 수 있다.
프로세스는 운영체제로부터 시스템 자원을 할당받는 단위이기도 한다. 프로그램이 실행되 어 적재될 때 Code, Data, Stack, Heap 영역을 할당받는다. 여기에 프로그램 카운터 PC를 포함하여 프로세스라고 한다.

## **프로세스의 문맥 context**

프로세스가 현재 어떤 상태에서 수행되고 있는지 정확히 규명하기 위해 필요한 정보를 말한다. 특정 시점에서 봤을 때, 이 프로세스가 어디까지 실행이 되고있는지 알 수 있다.

### **CPU 수행 상태를 나타내는 하드웨어 문맥**

-   Program Counter
-   각종 register

### **프로세스 주소 공간**

-   code
-   data
-   stack

### **프로세스 관련 커널 자료 구조**

-   프로세스 제어 블록 PCB (Process Control Block)
-   커널 내의 주소 Kernel stack

> **👩🏻‍💻 왜 이걸 알아야 하지?**  
> 현재의 컴퓨터는 time sharing을 통해 실행이 되기 때문에 CPU가 분배된다. 어느 시점까지 실행했는지 정확하게 알고 있어야 바로 그 다음 시점부터 실행이 가능해진다.

#### **Process Control Block (PCB)**

-   운영체제가 각 프로세스를 관리하기 위해 프로세스당 유지하는 정보
-   메모리 커널주소 공간의 data에 저장된다.
-   다음의 구성요소를 가진다. (구조체로 유지)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FtHJs3%2FbtrWYL62e9y%2FaDSye4wIUF2YmZop4xjBh1%2Fimg.png)

#### **OS 관리상 사용하는 정보**

1.  Process state : 계정 번호, CPU 할당 시간, CPU 사용 시간 등이 저장된다.
2.  Process ID (PID) : 운영체제 내에 여러 프로세스가 있기 때문에 프로세스를 구분하기 위한 구분자가 필요하다.
3.  scheduling information, priority : CPU 스케줄러가 준비 상태에 있는 프로세스 중 실행 상태로 옮겨야 할 프로세스를 선택할 때 프로세스의 우선순위를 기준으로 삼기 때문에 저장한다.

#### **CPU 수행 관련 하드웨어 값**

-   Program counter : 프로세스가 준비상태에서 실행상태 갈 경우 프로그램 카운터를 통해 다음 실행될 명령어의 위치를 알 수 있다. 또는 실행상태에서 준비상태로 갈 경우 프로그램 카운터에 저장하여 다음 실행될 명령어 위치를 저장한다.
-   registers : 프로세스가 실행 중에 사용했던 레지스터 정보( 누산기(Accumulator), 색인 레지스터, 스택 포인터 등)들이 저장된다. 이전 실행할 때 사용했던 레지스터 값들을 저장해야 다음에 실행할 수 있기 때문에 보관한다.

#### **메모리 관련**

-   Code, data, stack의 위치 정보 : 프로세스가 메모리의 어디에 있는지 알아야 하기 때문에 메모리 위치 정보가 필요하고 메모리 보호를 위해 사용되는 경계 레지스터, 한계 레지스터 값 등이 저장된다. 이외 세그먼테이션 테이블, 페이지 테이블 등의 정보도 포함된다.

#### **파일 관련**

-   open file descriptors… : 프로세스를 실행하기 위해 사용되는 입출력 자원, 오픈 파일 등에 대한 정보가 들어간다. 어떤 프로세스가 파일을 오픈하여 작업한다고 했을 경우 파일에 대한 정보가 필요하기 때문에 저장해야 한다.

## **프로세스의 상태**

-   컴퓨터 안에 CPU는 1개밖에 없다. 그러므로 CPU를 잡고 있는 프로세스는 매 순간 1개이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcWH72P%2FbtrWX55uEvF%2FOmLUecpTwww3Fx0k2jYex1%2Fimg.png)

### **Running**

-   CPU를 잡고 instruction을 수행중인 상태

### **Ready**

-   메모리 등 다른 조건을 모두 만족하며 CPU를 기다리는 상태
-   CPU를 얻었을 때 바로 instruction을 시행할 수 있는 상태
-   보통 이 상태에 있는 프로세스들이 CPU를 잡았다 놨다 하며 실행한다.

### **Blocked(wait, sleep)**

-   CPU를 주어도 당장 instruction을 수행할 수 없는 상태
-   Process 자신이 요청한 event가 즉시 만족되지 않아 이를 기다리는 상태
-   오래기다리는 작업이 필요하면 blocked 된다.
    -   공유 데이터 읽기
    -   I/O

### **그 외**

-   New : 프로세스가 생성중인 상태
-   Terminated : 수행(execution)이 끝난 상태. 그러나 아직 정리할 것이 남아있는 상태

---

## **🔗 참조 링크**

-   [Process & Thread](https://johnie.dev/computer-science/os/process-thread/)