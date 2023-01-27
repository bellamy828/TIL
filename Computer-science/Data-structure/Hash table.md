# Hash table
빠른 탐색을 위한 자료구조로 key-value 쌍의 데이터를 입력 받아 

Hash function에 key값을 넣어 얻은 해시값을 위치로 지정하여 key-value쌍을 저장함

## 시간복잡도

### 검색 / 저장 / 삭제 

- 모두 O(1)의 복잡도

<br>

## Direct Address Table vs Hash table

### Direct Address Table

- key 값을 index로 두고 value를 해당 index에 저장하는 방식
- key 값의 숫자 크기가 크면 앞의 무수히 많은 배열 공간이 낭비됨
- key 값이 숫자 외에 다른 자료형을 가질수 없음

### Hash table

- (key, value) 데이터 쌍을 저장하기 위해 적합한 자료구조
- key는 무조건 존재해야하고 중복되는 key는 없어야 한다.
- 숫자 이외의 자료형 key 값도 hash function을 통해 숫자(index)로 변환한다.
- hash table을 구성하는 key-value 데이터 쌍을 저장하는 각각의 공간을 slot 또는 bucket이라고 한다.

<br>

## Collision

### 원인

- 서로 다른 key의 해시값이 같아 충돌이 생김

### 예방

- collision이 일어나지 않도록 hash function을 잘 설계하는 것이 관건

### 해결 방법

- **Open addressing method**
    - 미리 정한 규칙에 따라 hash table의 비어있는 slot을 찾는다.
    - Seperate chaining(Linked list / Tree) 보다 메모리를 적게 사용한다.
    - 빈 slot을 찾는 방법은 Linear / Quadratic probing, Double hashing 등이 있다.
        - Linear / Quadratic Probing
            - 각각 총돌한 해시값으로 부터 (+1, +2, +3, …), (+1^2, +2^2, +3^2, …) 씩 건너 뛰어 비어 있는 slot을 조사한다.
            - 탐사할 때 각각의 이동폭이 일정하기 때문에 클러스터링 문제가 발생하기때문에 충돌 횟수가 많아지면 특정 영역에 데이터가 집중적으로 몰리는 Clustering이 발생한다.
                - Clustering되면 평균 탐색 시간이 증가하게 된다.
        - Double hashing
            - 2개의 해시 함수를 사용하여 클러스터링 발생 최소화
            - 하나는 초기 해시값을 얻을 때 사용, 다른 하나는 충돌이 발생했을 대 탐사 이동폭을 얻기 위해 사용한다.

<br>

- **Seperate chaining**
    - Linked list에 node(slot)을 추가하여 데이터를 저장한다.
    - 시간복잡도
        - 삽입
            - O(1) → Collision이 일어나면 Linked list에 다음 노드를 추가하여 key-value 쌍을 저장
        - 검색
            - 기본적으로 O(1)
            - worst case는 O(n) → n개의 모든 key가 같은 해시값을 갖게되면 worst case인 경우 길이 n의 Linked list 생성해야함
        - 삭제
            - 삭제할 node를 찾아야 하므로 검색의 시간복잡도와 동일
  
<br>
  
Reference: [https://www.nossi.dev/interview/cs/dsa#26463dc9-5d74-4f42-9263-aba5ad3c5ca1](https://www.nossi.dev/interview/cs/dsa#26463dc9-5d74-4f42-9263-aba5ad3c5ca1)
