# Process

Program(실행파일, 일의 순서가 적힌 문서)이 memory에 적재되어 CPU를 할당받아 실행되는 것을 process

## 개념

### process

- Program in execution
- 실행파일 형태로 존재하던 program이 memory에 적재되어 CPU에 의해 연산되는 것

### Memory 적재

- program이 CPU에 의해 실행(연산)되려면 memory에 적재된 상태여야 함
    - memory는 Code, Data, Stack, Heap 4개의 영역으로 구성, 각 process 마다 독립적으로 할당 받는다.
        - Code 영역 → 실행한 프로그램의 코드가 저장되는 메모리 영역
        - Data 영역 → 프로그램의 전역 변수와 static 벼수가 저장되는 메모리 영역
        - Heap 영역 → 프로그래머가 직접 공간을 할당(malloc)/해제(free)하는 메모리 영역
            - runtime에 메모리 영역의 크기가 정해짐
        - Stack 영역 → 함수 호출 시 생성되는 지역 변수와 매개 변수가 저장되는 임시 메모리 영역
            - compile time에 메모리 영역의 크기가 결정됨

### CPU의 연산 과정

- CPU가 프로그램의 코드를 읽어 연산해야 프로그램이 실행된다.
- CPU 내부의 Program Counter Register에 다음에 실행될 코드(명령어, instruction)의 주소값이 저장되어 있다.
    - PC Register는 memory에 적재된 process의 Code영역에 있는 명령어 중 다음번 연산에서 읽어야 할 명령어의 주소값을 순차적으로 가리키고, 해당 명령어를 읽어와서 CPU가 연산하면 process가 실행된다.
  
<br>

Reference: https://www.nossi.dev/interview/cs/os
