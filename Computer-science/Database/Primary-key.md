# Primary key

## Relation

- 데이터베이스에서 사용하기 위한 조건을 갖춘 Table
- 통상적으로 Relation과 Table 용어를 구분하지 않고 사용하기도 한다.

### 제약조건

- cell[^1]은 단일 값을 갖느다.
- 어떤 두 개 이상의 row도 동일하지 않다.

[^1]:cell: 데이터베이스에서 셀은 행과 열이 교차하는 테이블의 일부, 필드라고도 한다. row는 나란히 있는 하나 이상의 cell로 구성되고 열은 수직으로 서로 아래에 잇는 하나 이상의 셀로 구성된다.

### Table 구성

- Table, Relation
- Column, attribute
- row, tuple, record

## Primary key

### Super key

- 각 row를 유일하게 식별할 수 있는 하나 또는 **그 이상의 속성**의 집합
    - ex. 주민등록번호, (전화번호, 주민등록번호)의 집합, (이름, 주소, 성별)의 집합 등
- Table 안에서 row를 특정할 수 있는 고유의 값을 갖는다는 **유일성**만 만족하면 슈퍼키가 될 수 있다.

### Candidate key(후보키)

- 더이상 쪼개질 수 없는 Super key, 각 row를 유일하게 식별할 수 있는 최소한의 속성의 집합
    - 최소성: 모든 row를 유일하게 식별하는데 꼭 필요한 속성만으로 구성
        - ex. 위의 예시에서는 주민등록번호 column의 cell 각각이 해당할 수 있다.
- Primary key가 될 수 있는 다수의 column을 말한다.

### Primary key(기본키)

- Candidate key 중 선택한 main key, 각 row를 구분하는 유일한 column
    - 따라서 유일성과 최소성을 만족한다.
- `Null` 과 중복된 값 허용되지 않는다.
- Table 당 1개만 지정해야 한다.

### Alternative key(대체키)

- 2개 이상의 Candidate key 중 Primary key를 제외한 나머지 키 각각

### Foreign key(외래키)

- 다른 Table의 Primary key column을 참조하는 column

### Composite key

- Table에서 각 row를 식별할 수 있는 2개 이상의 column으로 구성된 Candidate key를 말한다.
    - 2개 이상의 column의 조합으로 유일성을 갖는 개념

  
  <br>

Reference

- [https://reference-m1.tistory.com/347](https://reference-m1.tistory.com/347)
- [https://www.nossi.dev/interview/cs/db](https://www.nossi.dev/interview/cs/db)
