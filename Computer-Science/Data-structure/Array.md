# Array

연관된 데이터를 **메모리상에 연속적이며 순차적**으로 **미리 할당된 크기**만큼 저장하는 자료구조

## 특징

- 고정된 저장 공간
- 순차적인 데이터 저장
- 장점
    - 요소를 찾거나 추가하는 작업이 빠름
    - 조회를 자주 해야하는 작업에 많이 사용
- 단점
    - 선언하면서 크기를 미리 정해야해서 메모리 낭비나 추가적인 overhead[^1]가 발생할 수 있음

[^1]: 어떤 처리를 하기 위해 들어가는 간접적인 처리 시간 · 메모리 등을 말함  
예를 들어 A라는 처리를 단순하게 실행한다면 10초 걸리는데, 안전성을 고려하고 부가적인 B라는 처리를 추가한 결과 처리시간이 15초 걸렸다면, 오버헤드는 5초가 된다.  
(Reference: https://ko.wikipedia.org/wiki/%EC%98%A4%EB%B2%84%ED%97%A4%EB%93%9C)
## 시간복잡도

| Operation | Time complexity |  |
| :---:| :---: | :---: |
| access | O(1) | index를 가지고 value를 조회하는 작업 |
| append | O(1) |
| 마지막 원소 delete | O(1) |
| insertion | O(n) |
| deletion | O(n) |
| search | O(n) | 요소의 value나 index를 탐색하는 작업 |

<br>

## Q. data가 많아서 미리 할당된 크기를 넘어서게 됐을 경우 해결 방법

- 기존 size 보다 더 큰 배열을 선언하고 데이터를 옮겨 할당, 기존 배열은 삭제, 이 과정을 자동적으로 수행하는 Dynamic Array 활용할 수도 있습니다.
- 또 다른 방법으로 size를 예측하기 어렵다면 Linked list를 활횽하여 데이터가 추가될 때마다 메모리 공간을 할당할 수 있습니다.

<br>

# Dynamic Array

자동적으로 resizing 하는 Array

## 특징

- size를 미리 고민할 필요가 없음
    - resizing: data를 계속 추가하다가 기존에 할당된 memory를 초과하게되면, size를 늘린 배열을 선언하고 그곳으로 모든 데이터를 옮김으로써 늘어난 크기의 size를 가진 배열이 됨
        - doubling: 기존의 2배 size를 할당, 기존 배열의 원소를 일일이 옮겨야하므로 O(n)
- Amortized time complexity
    - append 과정은 대부분 O(1)의 복잡도, resize(O(n))은 아주 가끔 발생
    - 가끔 발생하는 resize 시간을 자주 발생하는 O(1)의 작업에서 분담함으로써 전체적으로 O(1)의 복잡도

<br>

## Dynamic Array vs Linked List

### Linked List와 비교했을 때 Dynamic Array의 장점

- 데이터의 접근과 할당의 복잡도가 O(1)으로 상대적으로 빠릅니다.
    - index 접근할 때에 Array의 첫 요소의 주소값 + offset[^2]으로 random access 하기 때문입니다.

[^2]: 컴퓨터 과학에서 배열이나 자료 구조오브젝트 내의 오프셋(offset)은 일반적으로 동일 오브젝트 안에서 오브젝트 처음부터 주어진 요소나 지점까지의 변위차를 나타내는 정수형(Reference:https://ko.wikipedia.org/wiki/오프셋_(컴퓨터_과학))

- 배열의 마지막에 데이터를 추가하거나 삭제하는 것은 상대적으로 빠릅니다. (O(1))

### Linked List와 비교했을 때 Dynamic Array의 단점

- 배열의 마지막 부분이 아닌 곳에 데이터를 추가하거나 삭제할 경우 O(n)의 복잡도를 가져 속도가 느린편입니다.
    - 메모리상에 데이터를 연속적으로 저장하기 때문에 배열 중간에 데이터 추가/삭제할 경우 뒤에 있는 데이터를 모두 한 칸씩 shift 해야 합니다.
- resize할 때, 현저히 낮은 performance 가 될 수 있습니다.
- 마찬가지로 resize할 때 필요 이상으로 memory 공간을 할당하여 미처 다 사용하지 못한 메모리 공간이 생겨 메모리가 낭비될 수 있습니다.

  <br>
  
Reference(https://www.nossi.dev/interview/cs/dsa)
