# Heap

Priority Queue를 구현하기 위해 만들어진 자료구조, 완전 이진 트리의 일종

## 특징

- 완전 이진 트리로 구현
- 여러개의 값들 중에서 최댓값과 최솟값을 빠르게 찾을 수 있다.
- 부모 노드의 키 값이 자식 노드의 키 값 보다 항상 크거나 작도록 느슨한 정렬 상태를 유지한다.
- 힙 트리에서는 중복된 값을 허용한다.(cf. BST 에서는 중복 허용 X)

## 종류

### Max Heap

- 부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은 완전 이진 트리

### Min Heap

- 부모 노드의 키 값이 자식 노드의 키 값보다 작거나 같은 완전 이진 트리

## 구현

- 일반적으로 배열을 활용하여 힙을 구현한다.
- 보다 쉽게 구현하기 위해서 1번째 인덱스 부터 시작한다.
- 특정 위치의 노드 번호는 새로운 노드가 추가되어도 변하지 않는다. (ex. root의 오른쪽 자식 노드는 항상 3)
- 부모/자식 노드 관계
    - 왼쪽 자식의 인덱스 = 부모의 인덱스 x 2
    - 오른쪽 자식의 인덱스 = 부모의 인덱스 x 2 +1
    - 부모의 인덱스 = 자식의 인덱스 / 2

<br>
  

Reference: [https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html](https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html)
