# BST

모든 node의 왼쪽 자식 node는 그 부모 노드 보다 작은 값, 오른쪽 자식 node는 그 부모 노드 보다 큰 값을 갖도록 정렬된 Binary Tree[^1]

## 시간 복잡도

### **검색 / 저장 / 삭제**

- O(logn)

### worst case

- 한쪽으로 치우친 트리가 된 경우, Linked list와 동일한 O(n)
- 따라서 자동으로  트리의 높이를 작게 유지하는 자가 균형 이진 탐색트리(**[Self-balancing binary search tree](https://ko.wikipedia.org/wiki/%EC%9E%90%EA%B0%80_%EA%B7%A0%ED%98%95_%EC%9D%B4%EC%A7%84_%ED%83%90%EC%83%89_%ED%8A%B8%EB%A6%AC)**)를 사용하여 worst case를 예방할 수 있다.
    - ex. [AVL트리](https://ko.wikipedia.org/wiki/AVL_%ED%8A%B8%EB%A6%AC), [Red-black tree](https://ko.wikipedia.org/wiki/%EB%A0%88%EB%93%9C-%EB%B8%94%EB%9E%99_%ED%8A%B8%EB%A6%AC)
    - Java에서 hashmap의 seperate chaning으로 Linked list오 Red-black tree를 병행하여 저장?

## 특징

### BST의 조건

- root node의 값 보다 작은 값은 왼쪽 subtree, 큰 값은 오른쪽 subtree
- subtree도 위의 조건을 만족(Recursive)

### 정렬된 Tree

- 저장과 동시에 정렬을 하는 자료구조
- 새로운 데이터를 저장할 때, 일정한 규칙에 따라 저장

  
<br>

Reference: https://www.nossi.dev/interview/cs/dsa#47319de8-7aa8-4777-84ca-afc6bab17699

[^1]:Binary Tree: 각각의 노드가 최대 두 개의 자식 노드를 가지는 [트리](https://ko.wikipedia.org/wiki/%ED%8A%B8%EB%A6%AC_%EA%B5%AC%EC%A1%B0) [자료 구조](https://ko.wikipedia.org/wiki/%EC%9E%90%EB%A3%8C_%EA%B5%AC%EC%A1%B0)
