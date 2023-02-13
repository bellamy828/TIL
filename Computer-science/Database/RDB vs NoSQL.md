# RDB vs NoSQL

## NoSQL(Key-value storage system)

### 특징

- 최신 데이터가 꼭 관계형으로만 정의할 필요가 없는 경우도 많아졌다.
- Big data를 처리하기 위한 방법 중 하나
- SQL을 지원하지 않는다.
- Transaction을 지원하지 않는다.

### 종류

- Bigtable
- DynamoDB
- Cassandra
- MongoDB

## RDB vs NoSQL

|  |  |  |
| :---: | :--- | :--- |
| 데이터 저장 모델 | table | json document / key-value / 그래프 등  |
| 개발 목적 | 데이터 중복 감소 | 애자일 / 확장가능성 / 수정가능성 |
| 예시 | Oracle, MySQL, PostgreSQL 등 | MongoDB, DynamoDB |
| Schema | 엄격한 데이터 구조 | 유연한 데이터 구조 |
| 장점  | - 명확한 데이터 구조 보장 <br> - 데이터 중복 없이 한 번만 저장(무결성) <br> - 데이터 중복이 없어서 update 용이 | - 유연하고 자유로운 데이터 구조 <br> - 새로운 필드 추가 자유로움 <br> - Scale out(수평적 확장) 용이 |
| 단점 | - 시스템이 커지면 Join할 때 복잡한 Query 필요 <br> -  성능 향상을 위해 Scale up(수직적 확장)만 가능하여 비용이 큼 <br> - 데이터 구조가 유연하지 못함 | - 데이터 중복 발생 가능 <br> - 중복 데이터가 많기 때문에 데이터 변경시 모든 컬렉션에서 수정이 필요함 <br> - 명확한 데이터 구조 보장할 수 없음 |
| 사용 | - 데이터 구조 변경 필요가 없다는 것이 명확할 때 <br> - 데이터 update가 잦은 시스템(중복된 데이터가 없으므로 변경에 유리) | - 정확한 데이터 구조가 정해지지 않은 경우 <br> - 잦은 update가 필요 없는 경우(대신 조회가 많을 때) <br> - 데이터 양이 매우 많은 경우(Scale out 가능) |
  
<br>

Reference: https://www.nossi.dev/interview/cs/db
