# Queue

FIFO;선입선출 대기열

## 시간복잡도

- enqueue: 큐의 마지막에 데이터를 추가하기 때문에 O(1)
- dequeue: 큐의 맨 처음 데이터를 삭제하면 되기 때문에 O(1)

## 활용 예시

- 공유 프린터
- Cache
- 프로세스 관리
- BFS(너비우선탐색)

## 구현 방식

### Array-based queue

- enqueue와 dequeue 과정에서 남는 메모리가 발생할 수 있습니다.
- Circular queue 형식으로 구현하여 메모리를 좀 더 효율적으로 사용할 수 있습니다.

### List-based queue

- 재할당이나 메모리 낭비가 없습니다.

## 확장 & 활용

### Deque(Double-ended queue)

- 양쪽 방향에서 enqueue와 dequeue 가 가능합니다.

### Priority queue

- 우선 순위가 높은 순서로 dequeue 할 수 있습니다.

## Array-based vs List-based

|  | Array-based | List-based |
| :---: | --- | --- |
| 구현방식 | Dynamic array를 사용하여 계속되는 enqueue에 대응할 수 있고, Circular queue 형식으로 구현하여 메모리 낭비를 줄임 | 보통 Singly-linked list[^1]로 구현, enqueue는 append만 하면 되고 dequeue는 맨앞의 원소를 삭제하고 head를 변경 |
| 시간복잡도 | enqueue → Amortized O(1) <br> dequeue → O(1) | enqueue & dequeue → O(1) |
| 장점 | List-based 보다 전반적으로 나은 퍼포먼스 | resize 작업이 필요 없이 단순한 enqueue |
| 단점 | worst case(계속되는 enqueue로 인해 resize)의 경우 훨씬 더 느려질 수 있음 | enqueue 할 때 마다 memory allocation 해야하기 때문에 전반적인 runtime이 느릴 수 있음 |

Reference([https://www.nossi.dev/interview/cs/dsa#26463dc9-5d74-4f42-9263-aba5ad3c5ca1](https://www.nossi.dev/interview/cs/dsa#26463dc9-5d74-4f42-9263-aba5ad3c5ca1))

[^1]: Singly Linked list: 데이터들이 한쪽 방향으로만 연결 되어있는 것을 말합니다.  
데이터가 저장되는 객체를 node라고 하며, 가장 첫번째 node를 head라고 부릅니다.  
이런 특성 때문에, 데이터 탐색 중에 한번 지나친 node를 찾으려면 다시 head부터 탐색을 해야 합니다.  
(Reference: [https://codechacha.com/ko/singly-linked-list-java/](https://codechacha.com/ko/singly-linked-list-java/))
