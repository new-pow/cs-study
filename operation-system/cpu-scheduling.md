# CPU 스케줄링

- 어떤 프로세스가 대기해야 할 경우, 운영체제는 CPU를 그 프로세스로부터 회수해 다른 프로세스에 할당한다.
- 선택 절차는 **CPU 스케줄러**에 의해 수행된다.

## CPU 스케줄링을 하는 이유

- **다중 프로그래밍의 목적은 CPU 이용률을 최대화하기 위해 항상 실행 중인 프로세스를 가지게 하는데 있다.**
- **CPU 스케줄러는 실행 준비가 되어 있는 메모리 내의 프로세스 중에서 선택하여, 이들 중 하나에게 CPU를 할당한다.**

<aside>
❓ **실행 준비가 되어있는 프로세스??**

[4. Process](https://www.notion.so/4-Process-30f84388a60d4ef2b8e2b4ab544ebf17) 에서 프로세스 상태 키워드 참조

</aside>

## 목표

- `Batch System`: 가능하면 많은 일을 수행. 시간(time) 보단 처리량(throughout)이 중요
- `Interactive System`: 빠른 응답 시간. 적은 대기 시간.
- `Real-time System`: 기한(deadline) 맞추기.

## 기준

- CPU 이용률(`Utilization`): 어느 기간 동안 또는 특정 SNAPSHOT에서의 CPU의 이용률을 말한다.
- 처리량(`Throughput`): 단위 시간당 완료된 프로세스의 개수로써 나타낼 수 있다.
- 반환 (총처리) 시간(`Turnaround Time`): 프로세스의 제출 시간과 완료 시간의 간격을 반환시간(총처리) 시간이라고 한다.
- 대기 시간(`Waiting Time`): 대기 시간은 프로세스가 준비 큐에서 대기하면서 보낸 시간의 합이다.
- 응답 시간(`Response Time`): 하나의 Request를 제출한 후 첫 번째 Response가 나올 때까지의 시간이다.

## 선점 및 비선점 스케줄링 **Preemptive and Nonpreemptive Scheduling**

- CPU 스케줄링은 다음 4가지 상황에서 결정된다.
1. 한 프로세스가 실행 상태에서 대기 상태로 전환될 때 (I/O 발생) → 비선점 스케줄링
2. 프로세스가 실행 상태에서 준비 완료 상태로 전환될 때 (인터럽트 발생) → 선점 스케줄링
3. 프로세스가 대기 상태에서 준비 완료 상태로 전환될 때 (I/O 종료) → 선점 스케줄링
4. 프로세스가 종료할 때 → 비선점 스케줄링

### 선점스케줄링

시분할 시스템에서 타임 슬라이스가 소진되었거나, 인터럽트나 시스템 호출 종료시에 더 높은 우선 순위 프로세스가 발생 되었음을 알았을 때, 현 실행 프로세스로부터 강제로 CPU를 회수하는 것을 말한다.

- 처리시간 예측이 어렵다.
- 예시 : `Interrupt`, `I/O or Event Completion`, `I/O or Event Wait`, `Exit`

### 비선점스케줄링

일단 CPU가 한 프로세스에 할당되면 프로세스가 종료하든지, 또는 대기 상태로 전환해 CPU를 방출할 때까지 점유한다.

- 처리시간 예측이 용이하다.
- 예시 : `I/O or Event Wait`, `Exit`

## 디스패처 Dispatcher

- 디스패처(Dispatcher)는 CPU 코어의 제어를 CPU 스케줄러가 선택한 프로세스에 주는 모듈
- 이런 일들을 한다.
    - 한 프로세스에서 다른 프로세스로 문맥을 교환하는 일
    - 사용자 모드로 전환하는 일
    - 프로그램을 다시 시작하기 위해 사용자 프로그램의 적절한 위치로 이동(jump) 하는 일
- 디스패치 지연 (dispatch latency) : 하나의 프로세스를 정지하고 다른 프로세스를 수행시작하기까지 소요되는 시간
    
    ![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F587250b4-a040-4997-a4b9-9b98ce0bde6a%2FUntitled.png?id=bd665946-57f5-451b-a959-37a4ef718f6f&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)
    

# CPU 스케줄링 알고리즘 **CPU Scheduling Algorithm**

## **선입 선처리 알고리즘** FCFS **(First Come First Served)**

- **가장 먼저 요청한 프로세스**에 CPU를 할당해주는 방식이다.
- 비선점형(Non-preemptive) 스케줄링이다.
- 작성이 간단하고 이해하기 쉽다.
- 평균 대기 시간(Average Waiting Time)이 길어질 수 있다.
- `응답 시간`(Response Time)이 길어질 수 있다.
    - 처음으로 CPU를 얻는데 기다린 시간
- `반환 시간`(Turnaround Time) 면에서는 좋을 수 있다.
    - 프로그램이 제출 혹은 시작된 후 최종 결과물을 얻을 때 까지 소요되는 시간을 말합니다.
    - I/O버스트 + CPU버스트 + 기다린 시간 = Turnaround Time
- `Convoy Effect`(호위 효과)가 발생할 수 있다.
    - 호위 효과 : 하나의 긴 프로세스가 CPU가 양도하기를 다른 모든 프로세스들이 기다리는 것

## **최단 작업 우선 스케줄링 SJF(Shortest-Job-First) 스케줄링**

- 다음 CPU burst time의 길이를 고려해서 스케줄링을 결정하는 알고리즘이다.
- 비선점형과 선점형이 따로 존재한다.
- 비선점형에서는 실행되고 있는 프로세스는 끝까지 실행한다.
    - 앞의 프로세스가 실행되는 동안 새로운 프로세스가 준비 큐에 도착하면 선택이 발생한다.
- 선점형에서는 현재 실행되고 있는 프로세스의 남은 시간보다 도착한 다음 프로세스가 더 빨리 끝날 수 있는 프로세스라면 다음 프로세스를 실행하도록 바꾸게 된다. **SRTF**(Shortest Remaining Time First)라고도 부른다.
- SJF 스케줄링은 평균 대기 시간을 줄일 수 있다. 하지만 다음 프로세스의 CPU burst time을 예측하는 것이 어렵다는 문제가 존재한다.

- 비선점형 SJF

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Facfc1b56-80ba-4657-99ff-353a7e86a2db%2FUntitled.png?id=ac3776d5-28e1-4751-ac97-eb3b311c87c2&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

- 선점형 SJF

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F12295019-bdc4-4f90-8300-e3eb8988a1e3%2FUntitled.png?id=e6eb8d7f-4220-462c-ab39-bd9b2e61d1bf&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

## 우선순위 **Priority 스케줄링**

- 각각의 프로세스에 우선순위 넘버가 있다.
- 가장 높은 우선순위의 프로세스에 CPU를 할당한다.
- 선점형과 비선점형이 나뉜다.
- SJF도 우선순위 Priority 스케줄링이라고 할 수 있다. (다음 CPU burst time이 우선순위인 것처럼 작동하므로)

### 문제

- `무한 봉쇄(Indefinite blocking)` 혹은 `기아(Starvation)` 문제가 발생할 수 있다. 기아 문제란 낮은 우선순위의 프로세스가 절대 실행되지 않는 문제를 뜻함.
- 기아문제를 해결하기 위해서 `노화(aging)`를 사용할 수 있다.
    - 노화는 오랫동안 시스템에서 대기하는 프로세스들의 우선순위를 점진적으로 증가시킨다.
- 우선순위 스케줄링과 라운드 로빈 스케줄링을 결합하는 방법을 사용할 수도 있다.

## **라운드 로빈 스케줄링 Round Robin(RR) 스케줄링**

- 각각의 프로세스에 동일한 CPU 할당 시간을 부여해서 해당 시간 동안만 CPU를 이용하게 한다.
- 할당 시간 내에 처리를 완료하지 못하면 다음 프로세스로 넘어가므로 선점형 방식이다.
- n개의 프로세스가 있을 때 할당 시간을 q로 설정하면, 어떤 프로세스도 (n-1)q 시간 이상을 기다리지 않아도 된다.
- 응답 시간을 빠르게 할 수 있다는 장점이 있다.
- q가 커진다면 FCFS처럼 작동한다.
- q가 매우 작아지면 process sharing이라고 부른다. 이것은 n개의 프로세스가 프로세서 속도의 1/n 씩으로 작동함을 의미한다.
- 시간 할당량의 크기는 알고리즘의 성능과 Trade Off 관계임으로 문맥에 적절한 시간 할당량의 크기를 설정하자.

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F150478da-67ee-45a3-a34e-6510582ec3cf%2FUntitled.png?id=995ffffb-a273-4fe4-af06-9b38deef92c1&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

## 다단계 큐 **Multilevel Queue 스케줄링**

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fbee1c3ea-0f43-43a0-9b8a-f797b04bd85b%2FUntitled.png?id=bc3bda9a-a8a2-4783-8b36-d4f88e3f9e10&table=block&spaceId=1feb7462-9c33-4bf1-b0bb-7973d34ffaf2&width=2000&userId=180a704c-6552-4796-9dd2-ab125439ed98&cache=v2)

- `우선순위 스케줄링` + `라운드 로빈 스케줄링` 할때 사용됨
- 우선순위가 각 프로세스에 정적으로 할당되며 프로세스는 실행시간 동안 동일한 큐에 남아 있다.
- 각 큐는 각자의 스케줄링 알고리즘을 가지고 있다. == 자체 스케줄링 알고리즘을 구현할 수 있다.
- 각 큐 사이에서 프로세스들이 이동할 수 없다.
- 예시 : 일반적으로 `Foreground` 프로세스들은 Round Robin 방식을 사용하고, `Background` 프로세스는 FCFS를 사용한다.
    - `Foreground` 사용자 입력으로 제어받는 프로세스 (유저와 상호작용)
    - `Background` 사용자 입력과 상관없이 수행되는 프로세스
- 기아(Starvation) 문제가 발생할 수 있다.

## **다단계 피드백 큐 스케줄링 Multilevel Feedback Queue(MFQ)**

- Multilevel Queue와 비슷하지만, MFQ는 각 큐 간에 프로세스들이 이동할 수 있다.
- 다단계 피드백 큐 스케줄링 알고리즘은 Aging과 Starvation을 예방한다.
- 이 알고리즘은 특정 시스템에 부합하도록 구성이 가능함으로 **현대 사용되는 CPU 스케줄링 알고리즘 중 가장 일반적인 CPU 스케줄링 알고리즘이다.**
- 가장 좋은 스케줄러로 동작하기 위해서는 모든 매개변수 값들을 선정하는 특정 방법이 필요하기 때문에 가장 복잡한 알고리즘

---

- 참고
    - [https://imbf.github.io/computer-science(cs)/2020/10/18/CPU-Scheduling.html](https://imbf.github.io/computer-science(cs)/2020/10/18/CPU-Scheduling.html)
    - [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer Science/Operating System/CPU Scheduling.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/CPU%20Scheduling.md)