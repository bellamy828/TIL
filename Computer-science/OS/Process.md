# Process

Program(실행파일, 일의 순서가 적힌 문서)이 memory에 적재되어 CPU를 할당받아 실행되는 것

## What is Process?

### process

- Program in execution
- 실행파일 형태로 존재하던 program이 memory에 적재되어 CPU에 의해 연산되는 것

### Memory 적재

- program이 CPU에 의해 실행(연산)되려면 memory에 적재된 상태여야 함
    - memory는 Code, Data, Stack, Heap 4개의 영역으로 구성, 각 process 마다 독립적으로 할당 받는다.
        - Code 영역 → 실행한 프로그램의 코드가 저장되는 메모리 영역
        - Data 영역 → 프로그램의 전역 변수와 static 변수가 저장되는 메모리 영역
        - Heap 영역 → 프로그래머가 직접 공간을 할당(malloc)/해제(free)하는 메모리 영역
            - runtime에 메모리 영역의 크기가 정해짐
        - Stack 영역 → 함수 호출 시 생성되는 지역 변수와 매개 변수가 저장되는 임시 메모리 영역
            - compile time에 메모리 영역의 크기가 결정됨

### CPU의 연산 과정

- CPU가 프로그램의 코드를 읽어 연산해야 프로그램이 실행된다.
- CPU 내부의 Program Counter Register에 다음에 실행될 코드(명령어, instruction)의 주소값이 저장되어 있다.
    - PC Register는 memory에 적재된 process의 Code영역에 있는 명령어 중 다음번 연산에서 읽어야 할 명령어의 주소값을 순차적으로 가리키고, 해당 명령어를 읽어와서 CPU가 연산하면 process가 실행된다.

## What is Multi process?

### Multi Process

- 2개 이상의 process가 동시에 실행되는 것
- 각각의 process는 cpu와 memory를 공유한다.
    - memory → OS가 각각의 process 고유의 memory 영역에만 접근하도록 관리
    - cpu → 매 순간 하나의 process만 연산할 수 있지만, 매우 빠른 속도로 번갈아 가면서 process를 실행(Time sharing system), 사용자 입장에서는 동시에 실행되는 것처럼 보인다.
- Program counter register에는 다음에 실행될 명령어의 주소값이 저장되어 있고, pc register는 각 process의 code영역을 순서에 맞게 가리키면 CPU가 명령어를 읽어들이고 연산한다.

### Concurrency

- 하나의 CPU core가 여러 process를 짧은 시간 동안 번갈아가면서 연산하는 Time sharing system으로 실행하는 것
- 동시에 실행되는 것 처럼 보임

### Parallelism

- 2개 이상의 CPU core가 각각의 process를 연산하여 동시에 실행하는 것
- 실제로 동시에 여러 작업이 처리됨

### Context

- Time sharing system에서는 한 process가 매우 짧은 시간 동안 cpu를 점유하여 일정 부분 명령을 수행

→ 이후 다른 process가 cpu를 점유하여 명령어를 수행

→ 다시 처음 process의 차례가 되면 cpu를 점유하여 명령어를 수행

- Context는 이전에 각 process가 어디까지 명령을 수행했고, register에는 어떤 값이 저장되어 있는지에 대한 총체적인 정보이고 Process control block에 저장한다.

### Context switch

- 한 process에서 다른 process로 cpu의 제어권을 넘겨주는 것
    - 이 과정에서 이전 process의 상태를 PCB에 저장하고 새로운 process의 PCB를 읽어서 저장됐던 상태를 복구한다.

### PCB(Process control block)

- 운영체제가 특정 프로세스에 대한 중요한 정보를 저장하고 있는 자료구조
    - OS는 process 생성과 동시에 고유한 PCB를 생성하여 프로세스를 관리
- 프로세스의 중요한 정보가 포함되어 있기 때문에 일반 사용자가 접근하지 못하도록 보호된 메모리 영역안에 저장
- 일부 운영체제에서는 [Kernel](https://ko.wikipedia.org/wiki/%EC%BB%A4%EB%84%90_(%EC%BB%B4%ED%93%A8%ED%8C%85)) 스택에 위치한다.
    - Kernel
        - OS 또한 process이기 때문에 memory의 0xFFFFFFFF에 항상 적재되어있고, 시스템의 모든 것을 통제할 수 있는 운영체제의 핵심이다.
- PCB에 저장된 정보
    - Process State
        - new, running, waiting, halted…
            - running → process가 cpu를 점유하고 명령을 수행중인 상태
            - ready → cpu만 할당받으면 즉시 명령을 수행할 수 있도록 준비된 상태
            - (wait, sleep, blocked) → cpu를 할당받아도 명령을 실행할 수 없는 상태
                - ex. I/O 작업을 기다리는 경우
    - Process Number
    - Program counter
        - 해당 process의 다음에 실행할 명령어의 주소
    - Resgister
    - Memory limits 등
  
<br>

Reference
- [https://www.nossi.dev/interview/cs/os](https://www.nossi.dev/interview/cs/os)
- [https://eun-jeong.tistory.com/19](https://eun-jeong.tistory.com/19)
