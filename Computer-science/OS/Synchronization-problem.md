# Synchronization problem

## What is Synchronization problem?

### Synchronization problem

- 서로 다른 thread가 동일한 자원에 동시에 접근하여 엉뚱한 값을 읽거나 수정하는 문제
    - ex. `count++`의 처리 → 3개의 atomic operations
        1. `count` 변수의 값을 가져와서
        2. `count` 변수의 값을 1 증가시키고
        3. 변경된 `count` 값을 저장한다.
    - Race condtion: 시분할 시스템[^1]으로 작동하는 multi process / thread 시스템에서 2개의 thread가 동일한 데이터 `count`에 동시에 접근하여 연산하면 실행 결과가 접근이 발생한 순서에 따라 달라질 수 있다.
    - 따라서 한 순간에 하나의 process/thread만 해당자원에 접근하고 조작할 수 있도록 보장해야 함 → 동기화 작업 필요

### Critical section(임계 구역)

- 둘 이상의 process/thread가 동시에 동일한 자원에 접근하도록 하는 프로그램 코드 부분을 의미한다.
- 중요한 것은 한 process/thread가 자신의 임계 구역에서 수행하는 동안에는 다른 process/thread는 그 임계 구역에 접근할 수 없도록 임계 구역 내의 코드는 원자적으로(atomically) 실행되어야한다.
- 원자성을 갖기 위해서 각각의 process/thread는 자신의 임계 구역으로 진입하려면 Entry section에서 진입 허가를 요청해야하고 허가되면 임계 구역을 실행할 수 있다.
- 임계 구역이 끝나고 나면 exit section으로 퇴출한다.
- 대표적인 동기화 방법으로 Mutex, Smaphore가 있다.

### Mutex(Mutual exclusion)

- 공유 자원에 접근할 수 있는 prcoess/thread의 수를 1개로 제한, Race condtion을 방지하는 기법
- 임계 구역을 보호하고 경쟁 상황을 방지하기 위해 mutex lock을 사용한다.
    - 공유 자원을 점유하는 thread가 lock을 걸면 다른 thread는 unlock 상태가 될 때 가지 해당 자원에 접근할 수 없다.
    - process/thread는 임계 구역에 들어가기 전 반드시 lock을 획득하고, 빠져나올 때 반환해야 한다?
        - acquire() 함수가 lock을 획득하고 release() 함수로 반환
            
            ```java
            acquire()  // entry section
            
            ...  // critical section
            
            release()  // exit section 
            ```
            
- busy waiting 하는 동안 process/thread가 CPU 자원을 낭비할 수 있다.

### Semaphore

- Mutex와 다르게 공유 자원에 접근할 수 있는 process/thread의 개수가 2개 이상이 될 수 있다.
- 정수형 변수 S(emaphore) 값을 가용한 자원의 수로 초기화하고
- 변수 S(emaphore)에 동시에 접근 가능 한 process/thread의 개수를 저장하고, 임계 구역에 접근하면 개수 감소, S 값이 0이 되면 다른 process/thread는 접근 할 수 없다.
    
    ```java
    wait(S)  // entry section
    
    ...  // critical section
    
    signal(S)  // exit section 
    ```
    
- Semaphore 값으로 0, 1만 가질 수 있는 경우를 Binary semaphore라고 하는데, mutex와 거의 유사하게 작동한다.

[^1]:시분할 시스템: 여러 명의 사용자가 사용하는 시스템에서 컴퓨터가 사용자들의 프로그램을 번갈아가며 처리해줌으로써 각 사용자에게 독립된 컴퓨터를 사용하는 느낌을 주는 것으로, 라운드 로빈(Round Robin)방식이라고도 함

  
  <br>
  
Reference

- [https://pinelover.tistory.com/153](https://pinelover.tistory.com/153)
- [https://www.nossi.dev/interview/cs/os](https://www.nossi.dev/interview/cs/os)
