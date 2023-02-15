# Deadlock

## What is Deadlock?

### Deadlock

- 2개 이상의 Transaction이 각각 lock을 설정한 상태에서 서로의 lock이 걸린 데이터에 접근할 수 없어 무한 대기에 빠진 상태

## What is solution?

### 예방

- 각 Transaction에 필요한 데이터를 모두 Locking 하여 다 작업을 마친 후 다음 Transaction으로 넘어간다.
- Locking할 데이터가 많다면 사실상 모든 데이터를 Locking한 것과 같아 Transaction의 병행성 보장X

### 회피

- 자원을 할당할 때 time stamp를 사용하여 Deadlock을 회피한다.

### 탐지 / 회복

- Transaction이 실행되기 전에는 아무런 검사를 하지 않고, Deadlock이 발생하면 감지 / 회복하는 방법

  
  <br>

Reference: https://www.nossi.dev/interview/cs/db
