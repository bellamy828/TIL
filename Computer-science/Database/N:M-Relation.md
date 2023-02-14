# N:M Relation
## 1:N

- 관계형 데이터베이스에서 하나의 Entity(table)가 관계를 맺은 entity의 여러 객체를 가질 수 있는 구조
- 두 Table 간의 관계를 [Mapping cadrdinality](https://yunmap.tistory.com/entry/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-Relation%EC%9D%98-Mapping-Cardinality)로 표현한다.
- Primary key - Foreign key를 사용하여 관계를 맺는다.
    - 한 Table을 Foreign key가 다른 하나의 Table의 Primary key가 된다.
    - Primary key가 있는 Table의 정보가 변경된다고 해도 Foreign key가 있는 Table은 수정할 필요가 없어 효율으로 데이터베이스를 운영할 수 있다.

## N:M

- 양쪽 Entity 모두가 서로에게 1:N관계를 갖는 구조를 말한다.
- 보통 Mapping table을 통해서 관계를 맺는다.

  
Reference
- https://www.nossi.dev/interview/cs/db
- https://yunmap.tistory.com/entry/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-Relation%EC%9D%98-Mapping-Cardinality
