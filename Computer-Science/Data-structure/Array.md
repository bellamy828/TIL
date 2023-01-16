# Array

연관된 데이터를 **메모리상에 연속적이며 순차적**으로 **미리 할당된 크기**만큼 저장하는 자료구조

## 특징

- 고정된 저장 공간
- 순차적인 데이터 저장
- 장점
    - 요소를 찾거나 추가하는 작업이 빠름
    - 조회를 자주 해야하는 작업에 많이 사용
- 단점
    - 선언하면서 크기를 미리 정해야해서 메모리 낭비나 추가적인 overhead가 발생할 수 있음

## 시간복잡도

|  | Array |
| --- | --- |
| access | O(1) |
| append | O(1) |
| 마지막 원소 delete | O(1) |
| insertion | O(n) |
| deletion | O(n) |
| search | O(n) |

  
  Reference(https://www.nossi.dev/interview/cs/dsa)
