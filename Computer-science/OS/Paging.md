# 4. Paging

process가 할당받은 메모리 공간을 일정한 page 단위로 나누어 물리 메모리에서 연속되지 않는 서러도란 위치에 저장하는 메모리 관리 방법

## What is Paging?

### Paging

- process의 메모리 공간을 동일한 크기의 page 단위(frame)로 나누고 물리적 메모리상 서로 다른 위치에 각 page를 저장하는 메모리 관리 기법이다.
- address binding을 위해 모든 process가 각각의 주소 변환을 위한 page table을 갖는다.

### Memory fragmentation

- 물리적 메모리 공간이 작은 조각으로 나눠져 존재하지만 할당이 불가능한 상태
- process의 논리적 주소공간과 물리적 메모리가 같은 크기의 page 단위로 나누어지기 때문에 외부 단편화 문제가 발생하지 않는다.
- 하지만 process 주소 공간의 크기가 page 크기의 배수라는 보장이 없기 때문에 process의 주소 공간 중 가장 마지막에 위치한 page에서는 내부 단편화 문제가 발생할 수 있다.

  
<br>

Reference: [https://www.nossi.dev/interview/cs/os](https://www.nossi.dev/interview/cs/os)
