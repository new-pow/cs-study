## 들어가기 전 용어 정리

> 운영체제는 커널 모드(Kernel Mode)와 사용자 모드(User Mode)로 나뉘어 구동된다.

> \- 사용자 모드(User Mode)  
> : 유저가 접근할 수 있는 영역을 제한적으로 두며, 컴퓨터 자원에 함부로 침범하지 못하는 모드.  
>   
> \- 커널 모드(Kernel Mode)  
> : 모든 컴퓨터 자원에 접근할 수 있는 모드.  
>   
> \- 커널 (Kernel)  
> : 운영체제의 핵심 부분이자 시스템콜 인터페이스를 제공하며   
> 보안, 메모리, 프로세스, 파일 시스템, I/O 디바이스, I/O 요청 관리 등 운영체제의 중추적인 역할을 한다.  
> 즉, 파일 입출력, 프로세스 관리 등과 같이 운영체제의 기능을 담당

---

## 시스템 콜이 필요한 이유

> 일반 사용자(사용자 모드)는 커널에 접근할 수 없기 때문에   
> 원칙적으로는 파일 입출력, 프로세스 생성 등 커널의 기능을 사용하지 못한다.  
>   
> → **커널의 기능을 사용하기 위해, 운영체제에서 시스템 콜(system call)을 제공한다.**

##  시스템 콜(시스템 호출)이 무엇인가?

> 커널 영역의 기능을 사용자 모드가 사용 가능하게,   
> 즉, 프로세스가 하드웨어에 직접 접근해서 필요한 기능을 사용할 수 있게 해준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcNg7ge%2FbtrXaEzPwfq%2F5ZfqPaYDgt23oNKrJoMVHK%2Fimg.png)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcOdXRB%2FbtrW7Ui95Yi%2FwqgVvpAsLmrTgxZDLWCAb0%2Fimg.png)

> ※ modebit  
> : 시스템콜이 작동될 떄 modebit을 참고해서 유저 모드와 커널 모드를 구분한다.  
> 1 또는 0의 값을 가지는 플래그 변수이다.

-   인터럽트의 일종이다.
-   시스템 콜은 커널과 사용자 사이의 인터페이스 역할을 하는 것으로, 쉘(Shell)에서 명령어나 서브 루틴 형식으로 운영체제의 기능을 호출할 수 있다. 즉, **사용자가 직접 커널에 접근을 할 수 없기 때문에 시스템 콜을 활용**해야 한다.
-   보통 시스템 콜을 직접 사용하기 보단, 해당 시스템 콜을 사용해서 만든 각 언어별 라이브러리(API)를 사용한다.

→ 즉, 사용자 프로세스가 소프트웨어 인터럽트를 통해 커널을 이용하기 위한 서비스를 요청하는 하나의 방법.

→ 운영체제의 기능을 호출하는 함수

---

## 시스템 콜 처리과정

> 사용자 프로세스 → 시스템 콜 → libc.a → 0x80 인터럽트 발생 → 커널에서 처리

## 시스템 콜의 종류

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FHrkJz%2FbtrXfMXJEjT%2FC98kP6spSo4X9eDzq6HW1K%2Fimg.png)

1\. 프로세스 컨트롤

더보기

-   프로세스 생성 및 종료
-   메모리에 로드,실행
-   프로세스 속성 값 확인. 지정
-   wait 이벤트, signal 이벤트
-   메모리 할당

2\. 파일 매니지먼트

더보기

-   파일 생성, 파일 삭제
-   열기, 닫기
-   읽기,쓰기,Reposition
-   파일 속성 값 확인, 지정

3\. 디바이스 매니지먼트

더보기

-   디바이스 요청 및 해제
-   읽기,쓰기,Reposition
-   디바이스 속성 확인, 지정
-   비 물리적인 디바이스 해제 및 장착

4\. 정보 관리

더보기

-   시간 확인,시간 지정
-   시스템 데이터 확인, 지정
-   프로세스, 파일, 디바이스 속성 가져오기
-   프로세스 ,파일, 디바이스 속성 설정하기

5\. 커뮤니케이션

더보기

-   커뮤니케이션 연결 생성 및 삭제
-   메시지 송신,수신
-   상태 정보 전달
-   remote 디바이스 해제 및 장착

6\. 보안

더보기

-   Permission 획득
-   Permission 설정

---

## 시스템 콜 - 프로세스 컨트롤 

### 1\. fork()

> 프로세스를 복사하는 시스템 콜이며 Unix에서 새로운 프로세스를 만드는 역할을 한다.  
>   
> fork()는 부모 프로세스의 주소 공간을 그대로 복사하며,   
> 새로운 자식 프로세스를 생성하는 함수이다.   
> 주소 공간만 복사할 뿐이지, 부모 프로세스의 비동기 작업 등을 상속하지는 않는다.  
>   
> 그러나, 이상한 방식임.

-   fork() 시스템 호출 사용 코드

더보기

```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main(int argc, char *argv[]) {
    printf("pid : %d", (int) getpid()); // pid : 29146
    
    int rc = fork();					// 주목
    
    if (rc < 0) {
        exit(1);
    }									// (1) fork 실패
    else if (rc == 0) {					// (2) child 인 경우 (fork 값이 0)
        printf("child (pid : %d)", (int) getpid());
    }
    else {								// (3) parent case
        printf("parent of %d (pid : %d)", rc, (int)getpid());
    }
}
```

### 2\. wait

> child의 프로세스가 종료될 때까지 기다리는 작업.  
>   
> 자식 프로세스가 동작 중이면 상태를 얻어올 때까지 대기하며 종료된 후 상태를 얻음.  
> (즉, 부모 프로세스가 CPU점유권을 받았을 때 그때가 wait() 시스템콜이 끝나는 지점)

-   wait 사용 코드 : 위의 예시에 int wc = wait(NULL)만 추가함.

더보기

```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main(int argc, char *argv[]) {
    printf("pid : %d", (int) getpid()); // pid : 29146
    
    int rc = fork();					// 주목
    
    if (rc < 0) {
        exit(1);
    }									// (1) fork 실패
    else if (rc == 0) {					// (2) child 인 경우 (fork 값이 0)
        printf("child (pid : %d)", (int) getpid());
    }
    else {								// (3) parent case
        int wc = wait(NULL)				// 추가된 부분
        printf("parent of %d (wc : %d / pid : %d)", wc, rc, (int)getpid());
    }
}
```

### 3\. exec

> 단순 fork 는 동일한 프로세스의 내용을 여러번 동작할때 사용함.  
> child 에서는 parent 와 다른 동작을 하고 싶을 때 exec를 사용할 수 있음.  
>   
> 즉, exec()를 사용하는 목적은 프로세스의 구조체를 재활용하기 위해서이다.  
>   
> exec()를 실행하면 현재의 프로세스가 완전히 다른 프로세스로 전환됨  
>   
> 한마디로, **exec()는 새롭게 프로세스를 생성하는 함수**이다.

-   exec 사용 코드

더보기

```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main(int argc, char *argv[]) {
    printf("pid : %d", (int) getpid()); // pid : 29146
    
    int rc = fork();					// 주목
    
    if (rc < 0) {
        exit(1);
    }									// (1) fork 실패
    else if (rc == 0) {					// (2) child 인 경우 (fork 값이 0)
        printf("child (pid : %d)", (int) getpid());
        char *myargs[3];
        myargs[0] = strdup("wc");		// 내가 실행할 파일 이름
        myargs[1] = strdup("p3.c");		// 실행할 파일에 넘겨줄 argument
        myargs[2] = NULL;				// end of array
        execvp(myarges[0], myargs);		// wc 파일 실행.
        printf("this shouldn't print out") // 실행되지 않음.
    }
    else {								// (3) parent case
        int wc = wait(NULL)				// 추가된 부분
        printf("parent of %d (wc : %d / pid : %d)", wc, rc, (int)getpid());
    }
}
```

---

## 요약 겸 예상 질문

> Q. 시스템 콜이란 무엇인지 설명하시오.  
>   
> A. 시스템 호출(system call)은 운영 체제의 커널이 제공하는 서비스에 대해   
> 응용 프로그램의 요청에 따라 커널에 접근하기 위한 인터페이스이다.

> Q. fork()와 exec()가 사용되는 경우를 설명해보시오.  
> A. fork()를 사용하는 경우는 동일한 프로세스의 내용을 여러번 동작시킬 때이다.  
> exec()를 사용하는 경우는 child 에서는 parent 와 다른 동작을 하고 싶을 때이다.  
>   
> ++ 추가  
> Q. fork()를 사용할 경우 부모 프로세스와 자식 프로세스중 어떤것이 먼저 실행되는지?  
> A. fork()를 사용할 경우 두 프로세스의 실행 순서는 스케줄러가 관리하며,  
> 부모 프로세스와 자식 프로세스의 순서는 보장되지 않음.  
>   
> ++ 추가  
> Q. 자식 프로세스를 먼저 실행하고 싶을때, 순서를 보장해줄 수 있는 방법이 있는지?  
> A. wait() 시스템 콜을 사용하면 된다.

---

### 출처

-   [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/%5BOS%5D%20System%20Call%20(Fork%20Wait%20Exec).md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/%5BOS%5D%20System%20Call%20(Fork%20Wait%20Exec).md)
-   [https://chanhuiseok.github.io/posts/cs-3/](https://chanhuiseok.github.io/posts/cs-3/)
-   [https://luckyyowu.tistory.com/133](https://luckyyowu.tistory.com/133)
-   [https://ypangtrouble.tistory.com/entry/%EC%8B%9C%EC%8A%A4%ED%85%9C-%EC%BD%9CSystem-Call](https://ypangtrouble.tistory.com/entry/%EC%8B%9C%EC%8A%A4%ED%85%9C-%EC%BD%9CSystem-Call)