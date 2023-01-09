![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc8wUmo%2FbtrVDhSFiKC%2FD1m6cXdVzxA96BSXvPG4j1%2Fimg.png)

## **유닉스와 리눅스의 시작**

-   [1991년 리누즈 토발즈라는 대학생이 Linux 커널을 만듬](http://www.ddanzi.com/ddanziNews/200047221)
-   1969년 [유닉스의 탄생](http://www.ddanzi.com/ddanziNews/92939697)

---

## **유닉스 Unix**

### **유닉스의 주요 기능**

-   멀티태스킹 : 여러 프로그램을 동시에 실행할 수 있는 기능
-   가상메모리 : 프로그램이 물리적으로 사용 가능한 것보다 더 많은 메모리를 사용할 수 있도록 하는 시스템
-   파일 시스템 : 파일을 구성하고 저장하기 위한 계층적 시스템
-   셀 : 사용자가 운영 체제와 상호 작용할 수 있도록 하는 명령줄 인터페이스

---

## **리눅스 Linux**

리누스 토르발르가 1991년 유닉스 기반으로 개발한 컴퓨터 운영체제이다.

리눅스는 공개 소프트웨어라 회사 또는 그룹 등에서 커널 소스를 받아 OS를 직접 제작하여 사용된다.

따라서 특정 기관이 배포를 책임지는 것이 아니라 많은 배포판이 나온다.

리눅스는 많은 사용자들이 무료로 사용할 수 있다. 또한 오픈소스 운영체제로 많은 개발자들이 개발에 기여하고 있어 버그&오류 수정이 상대적으로 빨리 된다.

### **리눅스의 점유율 변화**

-   아래 항목 중 \[ic\]CentOS\[/ic\]와 \[ic\]Ubuntu\[/ic\] 의 개발환경을 세팅해보는 경험을 했었는데, 사실 기능 구현만 하는 입장에서는 명령어가 상이하다는 것이 가장 와닿는 차이점이었다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FpXWPl%2FbtrVDiYk2FX%2FS2PK3mltu6cjGcSGJ2uYm0%2Fimg.png)

---

## **유닉스 ↔️ 리눅스의 차이점**

-   가장 큰 차이점은 `리눅스 개발 커뮤니티`의 존재이다.
-   리눅스는 유닉스의 `클론`이지만 수년에 거쳐 Linux 코드베이스에는 많은 변경과 추가가 이루어졌다.

|   | **Unix** | **Linux** |
| --- | --- | --- |
| **사용 예시** | OS x, Solaris, 모든 리눅스 | Ubuntu, Fedora, Red Hat, Android 등 |
| **가격** | 유료 (무료 : Solaris) | 무료 (유료 버전도 저렴) |
| **사용자** | 대학, 큰 기업에서 주로 사용 | 모든 사람 |
| **개발과 배포** | 다양한 제조사. 대부분 AT&T   상업적 판매사와 비영리 단체에 의해 개발 | 리눅스 코드는 공유와 공동작업 등의   개발 특성을 가짐 |

---

### **👀 우리는 왜 유닉스와 리눅스를 배우는가?**

1. 개발자 소프트웨어에 특화되어있다.
우리가 프로그래머이고 개발자라면 리눅스는 반드시 배워야 한다.
지금 널리 사용되고 있는 운영체제 (OS)는 크게 NT(Windows)와 Unix 두개로 계열을 나눌 수 있다. 둘 중 무엇을 배워야 하는가 고민할 필요는 없다. 사실 운영체제는 사용자를 위한 것이라기보다는 **소프트웨어를 실행하기 위한 것**이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb4JVVw%2FbtrVzZMlmnm%2F0kRzhvxJ1LiCKXvdfWxMWk%2Fimg.png)

2. OS 사용률이 매우 높다.
아직 Desktop 용으로 유닉스는 사용이 미미하지만, 슈퍼 컴퓨터나 모바일, 웹클라이언트(자동차, 냉장고 등등)의 사용률은 유닉스 기반 OS가 압도적으로 많이 사용되고 있다.
유닉스는 대부분의 현대적 컴퓨터 운영 체제의 원형이 된 OS이다. 리눅스, 안드로이드, macOS, IOS, Xbox 등의 많은 운영체제가 유닉스를 뿌리로 하고 있다. 원래 멀티유저용 서버 운영체제나 현재는 개인용 데스크탑이나 임베디드 용으로 많이 사용된다.

#### OS 점유율 (데스크탑, 모바일, 태블릿, 콘솔)

Source: [StatCounter Global Stats - OS Market Share](https://gs.statcounter.com/os-market-share#yearly-2009-2023)

<script type="text/javascript" src="https://www.statcounter.com/js/fusioncharts.js"></script><script type="text/javascript" src="https://gs.statcounter.com/chart.php?all-os_combined-ww-yearly-2009-2023&amp;chartWidth=600"></script>

#### OS 점유율 (모바일, 태블릿, 콘솔)

Source: [StatCounter Global Stats - OS Market Share](https://gs.statcounter.com/os-market-share/mobile-tablet-console/worldwide/#yearly-2012-2023)

<script type="text/javascript" src="https://www.statcounter.com/js/fusioncharts.js"></script><script type="text/javascript" src="https://gs.statcounter.com/chart.php?mobile+tablet+console-os_combined-ww-yearly-2012-2023&amp;chartWidth=600"></script>

---

## **💪 개발자로서 최소한 알아야 하는 부분**

1.  일반적으로 리눅스에서 서비스를 돌릴 수 있는 능력이 필요하다.
2.  `터미널`을 이용하여 리눅스 서버에 접속해서 서비스 실행하고 관리할 수 있는 능력  
    -   Tomcat
    -   MySQL

이를 위해서 알고 있어야 하는 사전 지식은 다음과 같다.

-   Java JDK 설치 환경설정
-   Telnet/SSH/FTP 를 설치하고 관리하여 원격 연결시 사용
-   설치파일 관리자 사용
-   Bash/Shell 사용
-   프로세스 관리
-   사용자 관리
-   파일 관리 / 파일 편집
-   Linux 서버 설치
-   Linux/Unix 역사



---

## **참조 링크**

-   [유닉스와 리눅스의 많은 차이점](https://flaming.codes/ko/posts/the-many-differences-between-unix-and-linux)
-   [Unix Vs Linux: What Is Difference Between UNIX And Linux](https://www.softwaretestinghelp.com/unix-vs-linux/)
-   [리눅스 강의 1강. 왜 우리는 리눅스(Linux)를 배워야 하는가](https://youtu.be/TZjB94sA3IU)
-   [리눅스 강의 3강. 개발자가 알아야 할 리눅스의 필수 내용](https://youtu.be/Xd7IVMYnGUU)