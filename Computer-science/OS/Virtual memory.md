# Virtual memory
## What is Virtual memory?

### Virtual memory

- 물리적인 메모리 개념과 개발자 입장의 논리 메모리 개념을 분리하여 메모리 크기에 신경 쓰는 일을 최소화, 프로그램을 쉽게 작성할 수 있도록 한다.
- 운영체제는 가상 메모리 기법을 통해 프로그램의 논리적 주소 영역에서 필요한 부분만 물리적 메모리에 적재한다.
- 직접적으로 필요하지 않은 메모리 공간은 디스크(Swap 영역)에 저장한다.

### Demand paging

- 당장 사용할 주소 공간을 page 단위로 메모리에 적재하는 방법
- 특정 page에 대해 cpu의 요청이 들어온 후에 해당 page를 메모리에 적재한다.
- 당장 필요한 page만 적재하므로 메모리 사용량이 감소하고, 프로세스 전체를 메모리에 적재하는 입출력 오버헤드도 감소한다.
- Valid / Invalid bit를 두어 각 page가 메모리에 존재하는지 표시한다.

### Page fault

- CPU가 Invalid bit로 표시된 page에 엑세스 하는 상황
- 주소 변환을 담당하는 하드웨어인 [MMU(Memory Managemnet Unit)](https://ko.wikipedia.org/wiki/%EB%A9%94%EB%AA%A8%EB%A6%AC_%EA%B4%80%EB%A6%AC_%EC%9E%A5%EC%B9%98)가 Page fault trap을 발생시켜 Page fault를 처리한다.
    1. CPU가 페이지 N을 참조한다.
    2. Page table에서 페이지 N이 무효 상태임을 확인한다.
    3. MMU에서 Page fault trap을 발생시킨다.
    4. 디스크에서 페이지 N을 빈 프레임에 적재하고 page table을 업데이트한다. (Invalid → valid)

### Page replacement algorithm

- Page fault가 발생하면 요청된 page를 디스크에서 메모리로 가져오는데 이 때, 물리적 메모리 공간이 부족하여 메모리에 올라와 잇는 page를 디스크로 옮겨서 메모리 공간을 확보하는 작업이 Page replacement, 어떤 page를 교체할 것인지 결정하는 알고리즘이 Page replacement algorithm이다.
- Page fault를 최소화 할 수 있도록 참조될 가능성이 적은 page를 선택해서 교체하는 것이 성능을 향상시키는 방법이다.

| Algorithm | Desc |  |
| --- | --- | --- |
| FIFO (First In First Out) | 메모리에 올라온지 가장 오래된 page를 교체한다. |  |
| 최적 폐이지 교체 | 앞으로 가장 오랫동안 사용되지 않을 page를 찾아 교체한다. | 실제 구현 어려움 |
| LRU(Least Recently Used) | 가장 오랫동안 사용되지 않은 page를 교체한다 |  |
| LFU(Least Frequently Used) | 참조 횟수가 가장 적은 page를 교체한다.  | 비용대비 성능이 좋지 않아 잘 쓰이지 않음 |
  
  <br>
  
Reference: https://www.nossi.dev/interview/cs/os
