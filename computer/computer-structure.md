# 컴퓨터의 구조

- [컴퓨터의 구조](#컴퓨터의-구조)
  - [컴퓨터 구조의 분류](#컴퓨터-구조의-분류)
  - [컴퓨터가 이해하는 정보](#컴퓨터가-이해하는-정보)
    - [데이터](#데이터)
    - [명령어](#명령어)
  - [컴퓨터 부품](#컴퓨터-부품)
    - [CPU](#cpu)
    - [메모리](#메모리)
    - [보조기억장치](#보조기억장치)
    - [입출력장치](#입출력장치)
  - [기타 주요 요소](#기타-주요-요소)
    - [메인보드](#메인보드)
    - [시스템 버스](#시스템-버스)
    - [캐시 메모리](#캐시-메모리)
- [🔗 참고 링크](#-참고-링크)

---

<pre>
🤔 컴퓨터의 구조는 왜 알아야 하는 걸까?

1. 문제 해결 능력을 기를 수 있다.
문제가 생겼을 때 거리낌없이 컴퓨터 내부를 들여다볼 수 있어야 한다. 컴퓨터를 미지의 대상으로서 두려워하지 말고, 내려다보며 코딩하자.

1. 성능, 비용, 용량을 비교하며 프로그래밍을 할 수 있다.
결국 좋은 프로그래밍이란 '비용'에 대한 이야기를 빼놓을 수 없다. 최소의 비용으로 최선의 결과를 추구해야 한다.
</pre>

## 컴퓨터 구조의 분류
컴퓨터의 구조는 컴퓨터가 이해하는 정보, 컴퓨터의 핵심 (물리적)부품으로 나뉜다.

- 컴퓨터가 이해하는 정보
  - 데이터
  - 명령어
- 컴퓨터의 핵심 부품
  - CPU
  - 메모리
  - 보조기억장치 / 입출력장치

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcIv1QH%2FbtrVU9Uw3Wl%2FcpkQSIWkIIzKpkgnDJwLwk%2Fimg.png)
*컴퓨터의 구조. 모든 컴퓨터가 똑같지는 않지만, 필수 요소는 이렇게 가지고 있다.*

## 컴퓨터가 이해하는 정보
### 데이터
- 정적인 정보. 컴퓨터와 주고받는 혹은 내부에 저장된 정보를 `데이터`라 통칭하기도 한다.

### 명령어
- 컴퓨터를 실질적으로 움직이는 정보. 데이터는 명령어를 위한 일종의 재료이다.

## 컴퓨터 부품
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlkKIw%2FbtrVQOEoQQA%2Fkcrwia6wFTG5VWAfC6LnY0%2Fimg.png)
*이미지출처 : 위키백과. 이렇게 복잡한 Mainboard를 가장 추상화해서 가볍게 공부해보았다.*

### CPU
- 컴퓨터의 두뇌와도 같다. 메모리에 저장된 명령어를 읽고, 해석하고, 실행한다.
- 구성요소로는 연산장치, 제어장치, 레지스터가 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbGY0uS%2FbtrVTmAw9He%2F9IX2EIoIlorRE8hTnKnUV1%2Fimg.png)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FInyKO%2FbtrVTVC0dFN%2Fros6aWlbmTkCyCC9rv0yw1%2Fimg.png)

*CPU의 연산과정. 이미지와 같은 방식으로 반복하며 명령어를 한 줄 씩 실행한다.*
*이미지 출처 : 혼자서 공부하는 컴퓨터구조+운영체제.*

- 프로세서 (processor)라고도 한다.
- 프로그램을 실행
- 입력, 출력, 저장 장치 제어
 

### 메모리
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbPiXGo%2FbtrVWfGKbVQ%2FqQoRKDOIqgvsd8gSJJS3Y1%2Fimg.png)
*이미지 출처 : 혼자서 공부하는 컴퓨터구조+운영체제*

- 메모리는 `주소`라는 개념을 통해 내가 접근하고자 하는 데이터, 명령어에 접근할 수 있다.
- 프로그램는 실행되는 프로그램의 명령어와 데이터를 저장한다.
 
### 보조기억장치
- 메모리의 경우, 비싸고 전원이 꺼지면 저장된 내용을 잃는 휘발성 저장장치라는 단점이 있다.
- 반면 보조기억장치는 전원이 꺼져도 저장이 지속되고, 영구적으로 기억할 수 있다.
- 주기억장치에 비해 기억된 내용을 읽는 속도는 느리지만 대용량 기억도 가능하다.
- 메모리는 실행할 정보를 저장하고, 보조기억장치는 보관할 정보를 저장하는 역할을 나눠서 수행한다. 현재 사용하지 않는 프로그램은 보조기억장치에 저장하고, 작업이 수행될 때 주 기억 장치로 정보를 이동한다. (program loading)
- 디스크, USB 등이 보조기억장치이다.

 

### 입출력장치
- 컴퓨터 외부에 연결되어 컴퓨터 내부와 정보를 교환할 수 있다.
- 대표적인 예시로 키보드, 모니터, 마우스 등이 있다.

<pre>
👀 보조기억장치와 입출력장치는 뭐가 다를까?

사실상 딱 잘라 구분되는 개념은 아니다. 주변장치로 통칭하기도한다.
다만 보조기억장치는 메모리를 보조하는 특별한 입출력장치다.
</pre>

## 기타 주요 요소
### 메인보드
- 핵심 부품들을 연결하는 판(board)이다.
- 메인보드에 연결된 부품은 버스Bus 를 통해 정보를 주고 받는다.
- 다양한 종류의 버스가 있는데, 컴퓨터의 핵심 부품을 연결하는 버스 중 대표적인 예시는 시스템 버스이다.

### 시스템 버스
- 컴퓨터의 척추와 같은 역할을 한다.
- 시스템 버스 내부 구성
    - 주소 버스 : 주소를 주고받는 통로
    - 데이터 버스 : 명령어와 데이터를 주고받는 통로
    - 제어버스 : 제어 신호를 주고받는 통로

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbsINoC%2FbtrVWd3eALQ%2FDf4BFFCeqKjtplfXSULp10%2Fimg.png)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbM2qeR%2FbtrVUk92fHb%2Fi3FSVlD4A7cKTKkPMyKVn1%2Fimg.png)
*명령 수행 시 버스의 역할*
 

### 캐시 메모리
- 자주 사용되는 내용을 일시적으로 저장하여 프로그램 실행 속도를 향상시키기 위해 사용하는 메모리이다.
- CPU 캐시, 디스크 캐시, 웹 캐시 등 다양한 종류가 있다.
- 최근 CPU 캐시는 L1, L2, L3 cache로 구성된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FNBD0J%2FbtrVUjpLqQF%2Fs6OzYi1Nkf3pHqFi70UG1k%2Fimg.png)
메모리의 계층 구조도

---
# 🔗 참고 링크
- [컴퓨터구조] 시스템 캐시란?
- 혼자 공부하는 컴퓨터 구조+운영체제