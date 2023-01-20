# Stack

LIFO; 후입선출, 재귀적인 특징이 있어서 프로그램 개발에 자주 쓰이는 자료구조

## 시간복잡도

### push

- stack의 맨 뒤(위)에 데이터를 추가 O(1)

### pop

- push와 동일하게 stack의 맨 뒤(위)의 데이터를 삭제 O(1)

## 활용

- Call stack
- 후위 표기법 연산
- 괄호 유효성 검사
- 웹 브라우저 방문기록(뒤로가기)
- DFS(깊이우선탐색)

## Queue 2개를 이용하여 Stack 구현

### 구현

1. 모든 데이터를 첫 번째 Queue에 넣고, 마지막 요소를 제외한 모든 요소를 Dequeue 한다.
2. 첫 번째 Queue에서 Dequeue한 모든 요소를, 차례대로 두 번째 Queue에 넣는다.
3. 첫 번째 Queue에 남은 마지막 요소를 Dequeue 한다.
4. 다시 마지막 요소를 제외하고 비어있는 Queue에 넣고 하나 남은 마지막 요소를 Dequeue (반복)

```python
import queue

class Stack(obj):
		def __init__(self):
				self.oneQueue = queue.Queue()
				self.theOtherQueue = queue.Queue()

		def push(self, element):
				self.oneQueue.put(element)

		def pop(self):
				while self.oneQueue.qsize() > 1:
						self.theOtherQueue.put(self.oneQueue.get())

				temp = self.oneQueue
				self.oneQueue = self.theOtherQueue
				self.theOtherQueue = temp

				return self.theOtherQueue.get()
```

### 시간복잡도

- push() → O(1)
- pop() → oneStack의 마지막 요소를 제외한 n-1개의 요소를 theOtherStack으로 옮겨야 하므로 O(n). 
  
<br>
  
Reference(https://www.nossi.dev/interview/cs/dsa#26463dc9-5d74-4f42-9263-aba5ad3c5ca1)
