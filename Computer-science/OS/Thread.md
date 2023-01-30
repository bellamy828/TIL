# Thread

## 개념

### Thread

- 한 process 내에서 실행되는 동작(기능, function)의 단위
- thread는 process내에서 독립적인 기능, 즉 독립적으로 함수를 호출하는 것을 의미
    - 따라서 thread는 함수를 호출하기 위해서 인자 전달, Return Address 저장, 함수 내 지역변수 저장등을 위한 독립적인 Stack memory 공간이 필요하다.
- 각 thread는 속해있는 process의 Stack 메모리를 제외한 나머지 memory 영역을 공유할 수 있다.
- 각 thread는 독립적인 작업을 수행하기 위해서 PC Registser 값도 가지고 있다.
    - 한 process내에서도 thread 사이에서 Context switch를 하기 위해서 PC Register의 code addressf를 참조해야하기때문

### Multi-thread

- 하나의 process가 동시에 여러개의 일을 수행할 수 있도록 여러 개의 실행단위(thread)로 구분하고 Stack을 제외한 Code, Data, Heap 영역을 공유한다.

## Process vs Thread

### Process

- OS로부터 자원을 할당받는 작업의 단위
    - program이 하나의 process로 memory에 적재되어 cpu를 할당받아 실행된다.
- memory 공간에 code, data, heap, stack 영역이 있다.

### Thread

- process가 할당받은 자원을 이용하는 실행의 단위
    - 한 process 내에서 실행되는 동작의 단위
- process 내에서 stack 영역을 제외한 code, data, heap 영역을 공유한다.

Reference: [https://www.nossi.dev/interview/cs/os](https://www.nossi.dev/interview/cs/os)
