---
상태: 진행중
시작일: 2024-06-03
마감일: 2024-06-03
---
## 인덱스
> 테이블의 데이터에 대한 **검색 성능을 향상**시키기 위해 사용되는 구조
> 빠르게 정렬 그룹핑하기 위해 사용

특정 열(또는 열들)에 대한 데이터를 정렬된 형태로 저장하여 빠른 검색을 가능하게 합니다.  책의 색인처럼 작동, 데이터 검색 시에 Full Scan을 하지 않고 빠르게 접근할 수 있게합니다.

### 구조
 - [[B-Tree]]
 - 해시 테이블 구조

### Index를 쓰는 이유
**특정 조건을 만족하는 데이터를 빠르게 조회하기 위해서 사용합니다.**

아래 코드에서 SELECT, DELETE, JOIN등에서 WHERE나 ON에서 데이터를 빠르게 조회하기 위해 Index를 사용합니다.
```SQL
SELECT * FROM customer WHERE first_name = 'Minsoo';
DELETE FROM logs WHERE log_datatime < '2024-01-01';
SELECT * FROM employee E JOIN department D ON E.dept_id = D.id;
```

### Index 생성 방법
