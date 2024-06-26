---
상태: 완료
tags:
  - SQL
  - 트랜잭션
  - DB
시작일: 2024-06-16
마감일: 2024-06-19
---
## 트랜잭션이란
> 데이터베이스의 상태를 변화시키는 하나의 논리적인 작업 단위
> 데이터의 무결성, 일관성을 유지하기 위해 중요한 역할을 한다.

### 트랜잭션의 작업 단위
트랜잭션은 여러 작업을 하나의 단위로 묶어 처리한다. 이는 데이터베이스 시스템의 무결성을 유지하기 위해 중요합니다. 예) 은행 계좌간의 A계좌에서 금액을 차감하고 B계좌에 금액을 추가하는 두 개의 작업이 하나의 트랜잭션으로 처리된다.

### 트랜잭션 관리
DBMS에서 제공하는 기능으로, 다름과 같은 명령을 사용합니다.
- `BEGIN TRANSACTION` 또는 `START TRANSACTION`: 트랜잭션의 시작을 알림
- `COMMIT`: 트랜잭션 모든 작업이 성공적으로 완료되었음을 알리고, 변경 사항을 영구적으로 반영
- `ROLLBACK`: 트랜잭션 중 오류가 발생했을 때, 모든 변경사항을 취고, 데이터베이스를 트랜잭션 시작 전 상태로 되돌림


## ACID 특성

예제 시나리오: A가 B에게 100,000원을 송금한다.
1. A계좌에서 100,000원을 차감
2. B계좌에 100,000원을 추가

### Atomictiy(원자성)
트랜잭션의 모든 연산이 **완벽하게 수행되거나 전혀 수행되지 않아야**  한다.

A계좌에서 100,000원을 먼저 차감합니다. 중간에 에러가 발생해서 B에게 100,000원을 추가할 수 없게 되었습니다. 그럼 트랜잭션 RollBack을 하여 A계좌에서 차감했던 첫번째 연산 결과도 취소됩니다. 따라서 A계좌에서 100,000원이 차감되고 B계좌에 100,000원이 추가되는 상황을 방지할 수 있습니다.
```SQL
BEGIN TRANSACTION; 
UPDATE accounts SET balance = balance - 100000 WHERE account_id = 'A'; 
-- 오류 발생, 트랜잭션 롤백 
ROLLBACK;
```

트랜잭션 내의 **모든 연산은 하나의 단위, 부분적으로 수행되는 일은 없다.**
- 성공적으로 수행되면 Commit(커밋), 실패하면 Rollback(롤백)

### Consistency(일관성)
트랜잭션 전과 후에 데이터베이스가 일관된 상태를 유지해야 한다.
```SQL
BEGIN TRANSACTION; 
UPDATE accounts SET balance = balance - 100000 WHERE account_id = 'A'; 
UPDATE accounts SET balance = balance + 100000 WHERE account_id = 'B'; 
COMMIT;
```

일관성 보장: 트랜잭션 전후로 모든 데이터베이스 제약 조건(예: 각 계좌의 잔액이 음수가 되지 않는 등)을 만족해야 합니다.  트랜잭션이 완료된 후 A 와 B의 의 총 잔액은 변하지 않아야합니다.
A+B = 100이었다면 트랜잭션이 끝난 후에도 A + B = 100이어야합니다.

### Isolation(격리성)
각각 트랜잭션은 서로 간섭없이 독립적으로 수행되어야 한다.
```SQL
-- 트랜잭션 1: A가 B에게 100,000원 송금 
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ; 
BEGIN TRANSACTION; 
UPDATE accounts SET balance = balance - 100000 WHERE account_id = 'A'; 
-- 트랜잭션 1이 완료되기 전, 다른 트랜잭션은 A의 중간 상태를 볼 수 없음 

-- 트랜잭션 2: B가 자신의 잔액 조회 
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ; 
BEGIN TRANSACTION; 
SELECT balance FROM accounts WHERE account_id = 'B'; 
-- 트랜잭션 2는 트랜잭션 1이 완료되기 전까지 B의 잔액을 변경하지 않음 
COMMIT;
```

격리성 보장: 트랜잭션 1이 완료되기 전까지 트랜잭션 2는 B의 계좌에 대한 중간 상태를 볼 수 없습니다. 각 트랜잭션은 독립적으로 실행되는 것처럼 보입니다.


#### 트랜잭션 격리 수준에 따른 문제 발생
**더티 리드(Dirty Read)** : 하나의 트랜잭션의 커밋되지 않은 데이터를 다른 트랜잭션에서 읽을 수 있다.
- 첫 번째 트랜잭션이 트랜잭션이 롤백이 되면, 두 번째 트랜잭션은 무효한 데이터를 읽은 셈이된다. **이 때, 커밋되지 않은 데이터를 읽어왔기 때문에 문제가 발생한다.** 


**Non-repeatable Read**: 한 트랜잭션 내에서 동일한 쿼리의 결과가 다를 수 있다.
- 트랜잭션 A가 데이터를 읽은 후, 트랜잭션 B가 그 데이터를 업데이트하고 커밋합니다. 트랜잭션 A가 같은 데이터를 다시 읽을 때 변경된 값을 읽게됩니다.


**팬텀 리드(Phantom Read)**: 한 트랜잭션 내에서 범위 쿼리의 결과가 달라질 수 있다.
- 트랜잭션 내에서 새로운 행이 삽입되거나 삭제되어 쿼리 결과가 달라질 수 있습니다.


#### 트랜잭션 격리 수준
여러 트랜잭션이 동시에 처리될 때, **특정 트랜잭션이 다른 트랜잭션에서 변경하거나 조회하는 데이터를 볼 수 있게 허용할지 여부**를 결정하는 것

**격리수준이 높은** -> **낮은**
**SERIALIZABLE**  -> **REPEATABLE READ** ->  **READ COMMITTED** -> **READ UNCOMMITTED**

오른쪽으로 갈수록 격리 수준이 낮아지며, 동시 처리 성능이 높아진다.

왼쪽으로 갈수록 격리 수준은 높아지고, 동시 처리 성능은 낮아진다. 하지만, 데이터 부정합 문제 발생 확률이 줄어든다. **데이터 정합성과 성능은 반비례**한다.


#### SERIALIZABLE
트랜잭션을 무조건 **순차적으로 진행**시킨다. 트랜잭션이 끼어들 수 없으니 부정합 문제는 발생하지 않지만, 동시성이 아주 낮아져 그만큼 처리 속도가 느려진다.

#### REPEATABLE READ 
커밋된 데이터만 읽을 수 있고, 자신보다 낮은 트랜잭션 번호를 갖는 트랜잭션에서 커밋한 데이터만 읽을 수 있는 격리수준

#### READ COMMITTED
트랜잭션이 다른 트랜잭션에서 커밋된 데이터만 읽을 수 있는 격리수준으로 일반적인 비즈니스 애플리케이션에서 사용. 데이터의 정확성이 필요하지만 완전한 격리가 필요하지 않을 때 사용한다.

#### READ UNCOMMITTED(커밋되지 않은 읽기)
가장 낮은 수준으로, 트랜잭션이 완료되지 않은 다른 트랜잭션의 데이터를 읽을 수 있습니다.  더티 리드(Dirth Read)가 발생할 수 있습니다.


### Durability(지속성)
트랜잭션이 완료된 후에는 시스템 장애가 발생하더라도 그 결과가 영구적으로 반영되어야 한다.
```SQL
BEGIN TRANSACTION; 
UPDATE accounts SET balance = balance - 100000 WHERE account_id = 'A'; 
UPDATE accounts SET balance = balance + 100000 WHERE account_id = 'B'; 
COMMIT; 
-- 시스템 장애 발생
```

지속성 보장: 데이터베이스의 모든 변경 사항은 트랜잭션 로그에 기록됩니다. 이러한 로그는 트랜잭션이 커밋되기 전에 데이터베이스 시스템에 기록됩니다. 시스템 장애가 발생하더라도 로그를 통해서 커밋된 상태를 복구할 수 있습니다.

