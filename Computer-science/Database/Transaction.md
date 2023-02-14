# Transaction

- DBMS 또는 트랙잭션의 성공/실패가 분명하고 상호 독립적, 일관되고 믿을 수 있는 시스템에서의 상호작용의 최소 단위

## What is Transaction?

### Transaction

- 은행 계좌이체 → 송금처 출금 처리와 수신처 입금 처리가 하나의 묶음 형태로 작동해야하고, 입출금 성공 또는 아예 없던 일이 되어야한다. 이러한 분리될 수 없는 하나의 업무 처리 최소 단위를 Transaction이라고 한다.
- 데이터를 update하다가 장애가 일어나는 경우에도, 데이터를 복구하는 작업의 단위가 된다.
- DBMS는 서로 다른 작업이 동시에 같은 데이터를 다룰 때에도 각각의 작업을 분리하고 에러를 방지하도록 Transaction에 규칙을 부여한다.

### ACID

- Atomicity: Transaction은 전부 수행되거나 아니면 전부 실패해야한다.
- Consistency: Transaction 성공시 항상 일관성 있는 데이터 상태를 유지해야 한다.
- Isolation: 2개 이상의 Transaction이 동시에 수행되어도, 각각 다른 Transaction에 간섭 없이 독립적으로 수행되어야 한다. 하나의 data에 작업이 충돌하지 않도록 Concurrency control 한다.
- Durability: Transaction 성공한 데이터는 그 상태가 DB에 영원히 반영되어야 한다. 정전, 장애, 오류 등에 영향을 받지 않아야 한다.

### Concurrency control

- 갱신손실: 2개 이상의 Transaction이 하나의 data를 동시 update할 때, 어느 한 Transaction의 갱신이 무효화 되는 현상
- update중인 Transaction은 해당 데이터를 lock, 다른 Transaction이 수행되지 않도록 막는다.

## COMMIT and ROLLBACK

### COMMIT

- Transaction 작업이 완료됐다고 확정하는 명령어, 작업 결과를 DB에 반영한다.

### ROLLBACK

- 작업중 문제가 발생했을 때 Transaction 처리 과정에서 발생한 변경 사항 반영을 취소하고 이전 COMMIT 상태로 되돌린다.

  
  <br>

Reference: https://www.nossi.dev/interview/cs/db
