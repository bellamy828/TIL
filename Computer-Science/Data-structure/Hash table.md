# Hash table

빠른 탐색을 위한 자료구조로 key-value 쌍의 데이터를 입력 받아 

Hash function에 key값을 넣어 얻은 해시값을 위치로 지정하여 key-value쌍을 저장함

## 시간복잡도

- 검색 / 저장 / 삭제 → O(1)
- worst case -> O(n)

## Direct Address Table

- key 값을 index로 두고 value를 해당 index에 저장하는 방식
- key 값의 숫자 크기가 크면 앞의 무수히 많은 배열 공간이 낭비됨
- key 값이 숫자 외에 다른 자료형을 가질수 없음

## Hash table

- (key, value) 데이터 쌍을 저장하기 위해 적합한 자료구조
- key는 무조건 존재해야하고 중복되는 key는 없어야 한다.
- 숫자 이외의 자료형 key 값도 hash function을 통해 숫자(index)로 변환한다.
- hash table을 구성하는 key-value 데이터 쌍을 저장하는 각각의 공간을 slot 또는 bucket이라고 한다.

### collision

- 서로 다른 key의 해시값이 같아 충돌이 생김
- collision이 일어나지 않도록 hash function을 잘 설계하는 것이 관건
- 그럼에도 collision이 발생한 경우 seperate chaining 또는 open addressing으로 해결한다.
  
<br>
  
Reference: [https://www.nossi.dev/interview/cs/dsa#26463dc9-5d74-4f42-9263-aba5ad3c5ca1](https://www.nossi.dev/interview/cs/dsa#26463dc9-5d74-4f42-9263-aba5ad3c5ca1)
