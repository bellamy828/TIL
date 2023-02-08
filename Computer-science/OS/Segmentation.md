# Segmentation

## What is Segmentation?

### Segmentation

- process가 할당받은 메모리 공간을 논리적 의미 단위(segment)로 나누어서 연속되지 않는 물리 메모리 공간에 할당하는 메모리 관리 기법이다.
- 일반적으로 process 메모리 영역 중 Code, Data, Heap, Stack 등의 기능 단위로 segment를 정의 하는 경우가 많다.
- Paging의 page는 각각 동일한 크기를 갖는 반면에 sgement는 크기(limit)이 각각 다를 수 있다.
- address binding을 위해 모든 프로세스가 각각 주소 변환을 위한 segment table을 갖는다.

### Memory fragmentation

- segmentation 기법에서 segment의 크기만큼 메모리를 할당하므로 내부 단편화 문제가 발생하지 않는다.
- 하지만 서로 다른 크기의 segment들이 메모리에 적재되고 제거되는 일이 반복되면, 외부 단편화 문제가 발생할 가능성이 있다.

### Segmentation vs Paging

- paging은 일정한 크기의 단위로 나누어 할당을 하는데, 이에 반해 segmentation은 code, data, heap, stack등의 기능(의미)단위로 물리 메모리에 할당한다.
- paging의 경우 내부 단편화의 문제가 발생할 수 있는데, 이에 반해 segmentation은 외부 단편화의 문제가 발 생할 수 있다.

### Paged segmentation

- segmentation을 기본으로 하되 이를 다시 동일 크기의 page로 나누어 물리 메모리에 할당하는 메모리 관리 기법
- 프로그램을 의미 단위의 segment로 나누고 개별 segment의 크기를 page의 배수가 되도록 하는 방법
- 외부 단편화 문제를 해결하고, 동시에 segment 단위로 process 간의 공유나 process내의 접근 권한 보호가 이루어지도록 해서 paging 기법의 단점을 해결한다.

  
<br>  

Reference: [https://www.nossi.dev/interview/cs/os](https://www.nossi.dev/interview/cs/os)
