# 2. Linked list

데이터의 값과 다음 Node의 address를 저장할 수 있는 Node라는 구조체가 

메모리상에는 비연속적으로 저장되지만 다음 Node의 주소를 참조함으로써 논리적인 연속성을 갖는 자료구조

## 특징

- 장점
    - 메모리상에서 물리적으로 연속 저장하지 않아도 되므로 메모리 사용이 좀 더 자유롭습니다.
- 단점
    - 다음 참조할 address를 추가적으로 저장하기 때문에 각 데이터가 차지하는 메모리가 더 큽니다.

## 시간복잡도

- 배열의 중간에 데이터를 삽입/삭제하면 해당 인덱스 이후의 원소는 모두 shift해야하지만, Linked list에서 중간에 껴있는 데이터를 삽입 삭제할 때에는 다음 참조할 주소값만 변경하면 되므로 O(1)의 시간복잡도를 가집니다.

|  | Array |
| --- | --- |
| access | O(n) |
| append | O(n) |
| insertion | O(1) |
| deletion | O(1) |

<br>

  
Reference(https://www.nossi.dev/interview/cs/dsa)
