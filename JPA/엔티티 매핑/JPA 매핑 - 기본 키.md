---
상태: 완료
시작일: 2024-06-03
마감일: 2024-06-03
---
## 기본 키 매핑 어노테이션
- @Id
- @GeneratedValue
![](https://i.imgur.com/z93VOv1.png)

### IDENTITY 전략 - 특징
- 기본 키 생성을 데이터베이스에 위임
- 주로 MySQL, PostgreSQL, SQL Server, DB2에서 사용
- JPA는 보통 트랜잭션 커밋 시점에 INSERT SQL 실행
- AUTO_INCREMENT는 데이터베이스에 INSERT SQL을 실행한 이후 ID값을 알 수 있음
- IDENTITY 전략은 em.persist() 시점에 즉시 INSERT SQL 실행하고 DB에서 식별자를 조회

