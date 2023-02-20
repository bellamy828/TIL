# Index

## What is Index?

### Index

- 데이터베이스에서 Table의 검색 성능을 높여주는 대표적인 방법 중 하나로 보통 책의 마지막 부분에 제공되는 색인과 같은 역할을 하는 자료구조이다.
    - 책에서 특정 단어를 찾기 위해 처음 부터 전체를 훑어보는 작업(Full Table scan) → 색인에 정렬된 단어를 찾고 페이지를 확인하여 찾는 작업(Index scan)
- 일반적인 RDBMS는 B+Tree[^1] 구조로 된 Index를 사용하여 검색 속도를 향상시킨다.
- Full table scan 대비, 같은 SELECT ~ WHERE query 조회 작업이 훨씬 빨라진다.

### Index를 사용하는 이유

- Table에 많은 양의 데이터를 저장하면 특정 데이트를 찾을 때 최악의 경우 Table의 모든 row를 처음부터 끝까지 모드 접근해서 검색 조건과 일치하는지 비교하는 Full Table Scan을 해야할 수 있다.
- 특정 column에 대한 Index를 생성하면 Search key가 정렬되어 저장되기 때문에 조건 검색(SELECT ~ WHERE) 속도가 빨라진다.

### Index의 구조

- B-Tree, B+Tree, Hash, Bitmap으로 구현될 수 있고 많은 데이터 베이스 시스템에서 B+Tree구조를 갖고 있다.
- 특정 Column(Attribute)의 값을 기준으로 정렬하여 속성 값을 Search-key 값, 데이터의 물리적 위치를 저장한 값을 Pointer라고 하고 이렇게 정렬한 Index를 별도의 파일에 저장한다.

### Index의 단점

- 추가 저장 공간 필요
    - 보통 Table의 10% 크기를 갖느다.
- 느린 데이터 변경 작업
    - Lookup을 제외한 INSERT, UPDATE, DELETE 작업이 잦다면 성능이 나빠질 수 있다.
    - 보통 B+Tree 구조의 index는 데이터가 추가/삭제 될 때 마다 Tree의 구조가 변경될 수 있고, 결과적으로 Index를 재구성해야하기 때문에 추가적인 자원이 소모된다.

<br>

## Clustering index & Secondary index

### Clustering index

- 특정 Column을 Primary key로 지정하면 자동으로 Clustering index로 생성되어 해당 Column을 기준으로 정렬된다.
- 마치 사전처럼 Table 자체가 하나의 Index라고 볼 수 있다.

### Secondary index

- 일반적인 책의 색인처럼 별도의 공간에 생성한다.
- `CREATE INDEX`로 생성하거나 Unique key로 지정하면 생성할 수 있다.
    
    ```sql
    CREATE INDEX idx_name ON table_name(column_name)
    ```
    

[^1]: B+Tree: 동작 방식은 [B-Tree](https://ko.wikipedia.org/wiki/B_%ED%8A%B8%EB%A6%AC)와 유사하지만, B+Tree의 Leaf node는 Linked list 형태를 갖고 Binary search가 가능하다. 따라서 검색의 시간복잡도가 낮다.

<br>

Reference

- [https://velog.io/@emplam27/자료구조-그림으로-알아보는-B-Plus-Tree](https://velog.io/@emplam27/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-B-Plus-Tree)
- https://www.nossi.dev/interview/cs/db
