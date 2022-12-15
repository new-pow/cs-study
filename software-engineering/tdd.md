## 0. TDD(Test Driven Development)란?

> TDD란 Test Driven Development의 약자로 ‘**테스트 주도 개발**’이라고 한다.
> 

* 기존의 개발 프로세스 [그림 1] : 설계 → 코드 개발 및 테스트케이스 작성
* 테스트 주도 개발(TDD) [그림 2] : 테스트케이스 작성 → 실제 코드 개발 → 리팩토링

```
💡 즉, TDD와 일반적인 개발 방식의 가장 큰 차이점은, 
테스트 코드를 작성한 뒤에 실제 코드를 작성한다는 것
```

이러한 이유로 TDD를 Test First Development라고도 한다.

![](https://velog.velcdn.com/images/ummchicken/post/554c2b6d-1055-4762-bf59-16e91f521e64/image.png)

### 💡 비유를 해보면?

> 작가가 책을 쓰는 과정과 유사

| 책 | TDD |
| --- | --- |
| 목차를 구성 | 테스트코드 작성 |
| 초안을 작성 | 코드 개발 |
| 고쳐쓰기를 반복 | 코드 수정 |
| ∴ 반복적인 검토와 고쳐쓰기를 통해서 좋은 글이 완성 | ∴ 반복적인 테스트와 수정을 통해서 고품질의 소프트웨어를 만듦 |

## 1. **TDD를 왜 해야할까?**

💡 “**피드백**”과 “**협력**”이 중요하기 때문에 피드백과 협력이 자주 이루어진다면 더 좋은 결과가 나올 수 있기 때문

## 2. **TDD는 어떤 상황에서 해야할까?**

`만약, 어떤 부분에 대한 코딩을 여러 번 해봤고 결과가 어떻게 나올지 뻔하다면 TDD를 하지 않아도 된다.`

`또한 TDD를 했을 때 얻는 것이 적다면 TDD를 하지 않아도 된다.`

그렇다면 TDD는 어떤 상황에서 해야할까?

### 2 - 1. 처음해보는 프로그램 주제

> 나에 대한 불확실성이 높은 경우

### 2 - 2. 고객의 요구조건이 바뀔 수 있는 프로젝트

> 외부적인 불확실성이 높은 경우

### 2 - 3. 개발하는 중에 코드를 많이 바꿔야 된다고 생각하는 경우

### 4. 내가 개발하고 나서 이 코드를 누가 유지보수할지 모르는 경우

> 외부적인 불확실성이 즉, 불확실성이 높을 때 TDD를 하면 된다.
> 

## 3. TDD의 효과

```
💡 모든 애자일의 실천법은 피드백과 협력을 동시에 증진시킨다.
```

애자일이란?
→ 일정한 주기를 가지고 계속 검토해 나가며 **필요할 때마다 요구사항을 더하고 수정**하여 커다랗게 살을 붙이면서 개발

![](https://velog.velcdn.com/images/ummchicken/post/ec3cd0ec-4cff-4773-b698-ac667952c9e3/image.png)

### ❗ TDD 개발주기

- 위의 그림은 TDD의 개발주기를 표현한 것이다.

<**Red**>단계에서는 실패하는 테스트 코드를 먼저 작성한다.

<**Green**>단계에서는 테스트 코드를 성공시키기 위한 실제 코드를 작성한다.

<**Yellow**>단계에서는 중복 코드 제거, 일반화 등의 리팩토링을 수행한다.

1. 피드백 – **TDD를 하면 피드백이 증가**한다. 테스트 코드를 통해서 Green인지 Red인지 자주 확인할 수 있다.

2. 협력(핵심)

### 그렇다면 TDD는 왜 협력을 증진시킬까?

💡 “test”가 명사가 된다면 **공유가 쉬워진다**. 다른 사람의 코드를 **쉽게 접근 가능**하고, **이해가 빨라진다**. 그렇게 되면 다른사람의 **코드 의도를 확인**할 수 있게 된다.

## 4. TDD 예제

> 중간고사 45, 기말고사 25, 과제 30 점수를 합하여 결과를 성적을 내는 예제

### 4 - 0. 조건

성적 총합

- A ≥ 90
- 90 > B ≥ 80
- 80 > C ≥ 70
- 70 > D ≥ 60
- 60 > F

### 4 - 1. 단계 1

> 중간점수, 기말점수, 과제 점수를 받는 점수 입력을 받는 클래스를 작성

```java

public class GradeTest {
    
    @Test
    public void scoreResult() {
        
        Score score = new Score(35, 25, 25); // Score 클래스 생성 (점수 입력 받는 클래스)
        SimpleScoreStrategy scores = new SimpleScoreStrategy();
        
        String resultGrade = scores.computeGrade(score); // 점수 계산
        
        assertEquals("B", resultGrade); // 확인
    }
    
}
```

💡 현재는 **Score 클래스와 computeGrade() 메소드가 구현되지 않은 상태**다. 
(테스트 코드로만 존재!)
→ 테스트 코드에 맞춰서 코드 개발을 진행하자

### 4 - 2. 단계 2

> **점수를 저장**할 Score 클래스를 생성

```java

public class Score {
    
    private int middleScore = 0;
    private int finalScore = 0;
    private int homeworkScore = 0;
    
    public Score(int middleScore, int finalScore, int homeworkScore) {
        this.middleScore = middleScore;
        this.finalScore = finalScore;
        this.homeworkScore = homeworkScore;
    }
    
    public int getMiddleScore(){
        return middleScore;
    }
    
    public int getFinalScore(){
        return finalScore;
    }
    
    public int getHomeworkScore(){
        return homeworkScore;
    }
    
}
```

### 4 - 3. 단계 3

> **점수 계산을 통해 성적**을 뿌려줄 computeGrade() 메소드를 가진 클래스를 만든다.

1. 우선 인터페이스를 구현하자

```java

public interface ScoreStrategy {
    
    public String computeGrade(Score score);
    
}
```

1. 인터페이스를 가져와 오버라이딩한 클래스를 구현

```java

public class SimpleScoreStrategy implements ScoreStrategy {
    
    public String computeGrade(Score score) {
        
        int totalScore = score.getMiddleScore() + score.getFinalScore() + score.getHomeworkScore(); // 점수 총합
        
        String gradeResult = null; // 학점 저장할 String 변수
        
        if(totalScore >= 90) {
            gradeResult = "A";
        } else if(totalScore >= 80) {
            gradeResult = "B";
        } else if(totalScore >= 70) {
            gradeResult = "C";
        } else if(totalScore >= 60) {
            gradeResult = "D";
        } else {
            gradeResult = "F";
        }
        
        return gradeResult;
    }
    
}
```

이제 테스트 코드로 돌아가서, 실제로 통과할 정보를 입력해본 뒤 결과를 확인해보자

💡 테스트 코드에 작성된 클래스 정보를 **통과할 정도로 입력을 한 뒤**, 리팩토링 작업 (예외처리, 중복제거, 추가 기능)을 하며 반복한다.

통과가 가능한 정보를 넣고 실행하면, 아래와 같이 에러 없이 제대로 실행되는 모습을 볼 수 있다.

![](https://velog.velcdn.com/images/ummchicken/post/11b49d0e-a75a-467d-b6b0-9aa7f2dd3050/image.png)


## 5. 굳이 필요하나요?

딱봐도 귀찮아 보인다. 
저렇게 확인 안 해도 결과물을 알 수 있지 않냐고 반문할 수도 있다.
하지만 예시는 간단하게 보였을 뿐, 
실제 실무 프로젝트에서는 **다양한 출력 결과물이 필요**하고, 
**원하는 테스트 결과가 나오는 지 확인하는 과정**은 필수적인 부분이다.

TDD를 활용하면, 
처음 시작하는 단계에서 테스트케이스를 설계하기 위한 **초기 비용이 확실히 더 들게 된다.** 
하지만 개발 과정에 있어서 **'초기 비용'보다 '유지보수 비용'이 더 클 수 있다는 것을 명심**하자

💡 또한 **안전성이 필요한 소프트웨어 프로젝트**에서는 개발 초기 단계부터 확실하게 다져놓고 가는 것이 중요!

## 6. TDD 개발 방식의 장점

### 6 - 1. 보다 튼튼한 객체 지향적인 코드 생산

> TDD는 코드의 재사용 보장을 명시, 따라서 TDD를 통한 소프트웨어 개발 시 기능 별 철저한 모듈화가 이뤄진다.

이는 **종속성과 의존성이 낮은 모듈**로 조합된 소프트웨어 개발을 가능하게 하며 
필요에 따라 모듈을 추가하거나 제거해도 소프트웨어 전체 구조에 영향을 미치지 않게 된다.

### 6 - 2. 재설계 시간의 단축

> 이는 **유닛 테스팅**을 하는 이점이기도 하다.

예를 들면, 
사용자의 데이터가 잘못 나온다면 DB의 문제인지, 비즈니스 레이어의 문제인지 UI의 문제인지 
실제 모든 레이러들을 전부 디버깅 해야하지만, 
TDD의 경우 자동화 된 유닛테스팅을 전재하므로 특정 버그를 손 쉽게 찾아낼 수 있다.
즉, 자동화 도구를 이용한 TDD 테스트케이스를 단위 테스트로 사용이 가능하다.
(자바는 JUnit, C와 C++은 CppUnit 등)

```
💡 단위 테스트란(Unit Test)란?
→ 말 그대로 한 단위(일반적으로 class)만을 테스트하는 것
```

### 6 - 3. 작업과 동시에 테스트를 진행하면서 실시간으로 오류 파악이 가능함
시스템 결함 방지

### 6 - 4. 짧은 개발 주기를 통해 고객의 요구사항 빠르게 수용 가능
> 피드백이 가능하고 진행 상황 파악이 쉬움

## 7. TDD 개발 방식의 단점
> 가장 큰 단점은 바로 생산성의 저하

```
※ 참고
SI 프로젝트에서는 소프트웨어의 품질보다 납기일 준수가 훨씬 중요하기 때문에 TDD 방식을 잘 사용하지 않는다.
```

### 7 - 1. 기존 개발 프로세스에 테스트케이스 설계가 추가되므로 생산 비용 증가

### 7 - 2. 테스트의 방향성, 프로젝트 성격에 따른 테스트 프레임워크 선택 등 추가로 고려할 부분의 증가

---

### 출처

- [링크](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Software%20Engineering/TDD(Test%20Driven%20Development).md)
- [링크](http://clipsoft.co.kr/wp/blog/tddtest-driven-development-%EB%B0%A9%EB%B2%95%EB%A1%A0/)
- [링크](https://wooaoe.tistory.com/33)