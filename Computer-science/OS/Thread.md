#  Thread

## 개념

### Thread

- 한 process 내에서 실행되는 동작(기능, function)의 단위
- thread는 process내에서 독립적인 기능, 즉 독립적으로 함수를 호출하는 것을 의미한다.
- 각 thread는 속해있는 process의 Stack 메모리를 제외한 나머지 memory 영역을 공유할 수 있다.
- 각각의 thread는 독립적인 잡업을 수행하기 위해서 각자의 스택과 PC Registser 값을 가지고 있다.

### Multi-thread

- 하나의 process가 동시에 여러개의 일을 수행할 수 있도록 여러 개의 실행단위(thread)로 구분하고 Stack을 제외한 Code, Data, Heap 영역을 공유한다.
