# Multi process & Multi thread

## Multi process vs Multi thread

|  | Multi process | Multi thread |
| --- | --- | --- |
| Memory 사용 | 상대적으로 많은 메모리 공간 필요 | 상대적으로 적은 메모리 공간 필요 |
| CPU time | 상대적으로 긴 CPU time | 상대적으로 짧은 CPU time |
| Context switching | 상대적으로 느림 | 상대적으로 빠름 |
| 안정성 | 상대적으로 안정적 | 상대적으로 안정성 낮음 |

## Multi process

### 장점

- memory를 구분하여 따로 운용해야 할 때 유리하다.
- 단일 process가 죽더라도 다른 process에 영향을 끼치지 않아 안정성이 높다.

### 단점

- 상대적으로 많은 memory 공간과 CPU time 필요
- IPC(Inter Process Communication) 프로스세간 통신을 위해서 overhead가 발생한다.

### IPC(Inter Process Communication)

- process는 독립적인 주소 공간을 갖기 때문에 다른 process의 주소 공간 참조할 수 없음
- 따라서 데이터를 주고 받기 위해서 IPC를 사용
    - Share memory
        - Share memory, [POSIX](https://ko.wikipedia.org/wiki/POSIX)가 있다.
        - process간 주소 공간의 일부를 공유하고 공유한 메모리 영역에 읽기/쓰기를 통해 통신 수행
        - process → kernel 공유 메모리 할당 요청하면 메모리 공간을 할당해준다.
        - 공유 메모리 영역이 구축된 이후 모든 접근이 일반적인 메모리 접근으로 취급되어 더이상 kernel의 도움 없이 각 process가 접근할 수 있다.
        - 따라서 커널의 관여 없이 데이터 통신이 가능하기 때문에 속도가 빠르다.
        - 하지만 동시에 같은 메모리 위치에 접근하게 되면 일관성 문제가 발생할 수 있다.
            - 커널이 관여하지 않기 때문에 각 process가 동기화 문제를 책임져야 한다.
    - Message passing
        - pipe, socket, message queue등이 있다.
        - 통상 [System call](https://ko.wikipedia.org/wiki/%EC%8B%9C%EC%8A%A4%ED%85%9C_%ED%98%B8%EC%B6%9C)을 사용하여 구현하고 kernel을 통해 send/receive (message) 두 연산을 제공 받는다.
            - ex. process1 → kernel로 message를 보내면, kernel이 process2에게 message 보내줌
        - 구현하기 쉽고 충돌을 회피할 필요가 없기 때문에 적은양의 데이터를 교환하는데 유용하다.
            - kernel에서 제어 및 동기화를 해주기 때문에 안전하다.
        - Share memory 방식 보다는 속다가 느리다.

## Multi thread

### 장점

- Context switcing과 데이터 공유가 빈번한 경우
- memoryd와 시스템 자원을 효율적으로 사용하고자 할 때 유리하다.
    - process를 생성하고 자원을 할당하는 등의 system call 생략할 수 있다.
- Context Switching 할 때 캐시 Cache memory 초기화가 필요 없어 상대적으로 속도가 빠르다.
- 데이터 통신면에서 IPC 보다 통신 비용이 적기 때문에 overhead가 적다.

### 단점

- 동기화 등의 이유로 싱글 코어 멀티스레딩은 스레딩 생성 시간이 오히려 overhead로 작용해서 단일 스레드 보다 느리다.
- 단일 thread의 장애로 전체 thread가 종료될 위험이 있다.
- 데이터와 힙 영역을 공유하기 때문에 어떤 스레드가 다른 스레드에서 사용 중인 변수나 자료구조에 접근하여 엉뚱한 값을 읽어오거나 수정할 수 있다.
    - 따라서 프로그램을 설계할 때 주의가 필요, Synchronization 작업이 필요하며 여러가지 동기화 기법이 있다.
        - | 기법 | 설명 |
          | --- | --- |
          | 임계 영역(critical section) | 공유자원에 대해 오직 한 스레드의 접근만 허용(한 프로세스에 속한 스레드 간에만 사용 가능) |
          | 뮤텍스(metex) | 공유 자원에 대해 오직 한 스레드의 접근만 허용(서로 다른 프로세스에 속한 스레드 간에도 사용 가능) |
          | 이벤트(event) | 사건 발생을 알려 대기 중인 스레드를 깨운다. |
          | 세마포어(semaphore) | 한정된 개수의 자원에 여러 스레드가 접근할 때, 자원을 사용할 수 있는 스레드 개수를 제한한다. |
          | 대기 가능 타이머(waitable timer) | 정해진 시간이 되면 대기 중인 스레드를 깨운다. |

  <br>

Reference

- [https://www.nossi.dev/interview/cs/os](https://www.nossi.dev/interview/cs/os)
- [https://eun-jeong.tistory.com/20](https://eun-jeong.tistory.com/20)
- [https://12bme.tistory.com/68](https://12bme.tistory.com/68)
- [https://velog.io/@octo__/스레드-동기화](https://velog.io/@octo__/%EC%8A%A4%EB%A0%88%EB%93%9C-%EB%8F%99%EA%B8%B0%ED%99%94)
