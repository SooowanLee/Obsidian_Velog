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
 - **B-Tree**
 - **해시 테이블 구조**

### Index를 쓰는 이유
**특정 조건을 만족하는 데이터를 빠르게 조회하기 위해서 사용합니다.**

아래 코드에서 SELECT, DELETE, JOIN등에서 WHERE나 ON에서 데이터를 빠르게 조회하기 위해 Index를 사용합니다.
```SQL
SELECT * FROM customer WHERE first_name = 'Minsoo';
DELETE FROM logs WHERE log_datatime < '2024-01-01';
SELECT * FROM employee E JOIN department D ON E.dept_id = D.id;
```

### Index 생성 방법
#### 테이블에 데이터가 이미 존재
중복을 허용하는 인덱스
- `CREATE INDEX player_name_idx ON player(name);`

중복을 허용하지 않는 인덱스
- `CREATE UNIQUE INDEX team_id_backnumber_idx ON player(team_id, backnumber);`

#### 테이블 생성시에 인덱스 적용
CREA TABLE에서 INDEX를 적용하면 INDEX 이름을 생략해도 DBMS에서 자동으로 이름을 생성해준다.
```sql
CREATE TABLE player(
	id INT PRIMARY KEY,
	name VARCHAR(20) NOT NULL,
	team_id INT,
	backnumber INT,
	INDEX player_name_idx(name),
	UNIQUE INDEX team_id_backnumber_idx(team_id, backnumber)
);
```
두 개 이상의 컬럼으로 구성된 인덱스를 multicolumn index, composite index라고 한다.

대부분의 RDBMS에서는 primary key에는 index가 자동 생성된다.

### 테이블에 걸린 인덱스 보기
`SHOW INDEX FROM player`
![](https://i.imgur.com/tefqTIZ.png)

`Table` : 테이블 이름
`Non_unique`: 인덱스의 유니크 여부
`Key_name`: Index 이름
`Seq_in_index`: 인덱스 내에서 열(column)의 순서
- Seq_in_index가 1, 2인것으로 보아 multicolumn index라는 걸 알 수 있다.
`Column_name`: 컬럼 이름
`Null`: 해당 INDEX의 Attribute의 Null 허용 여부

### [[B-Tree]] 기반의 index가 동작하는 방식
B-Tree는 KEY=VALUE 형태로 데이터를 저장하고 있습니다.
KEY에는 컬럼의 값을 가지고 있고, VALUE에는 값의 주소를 가지고 있습니다.

MEMBERS 라는 테이블의 a컬럼을 기준으로 인덱스를 생성합니다.
![](https://i.imgur.com/UbtWgze.png)

인덱스는 기본적으로 정렬해서 값을 가지고 있습니다.

여기서 `where a = 8`로 a를 조회한다면 
![](https://i.imgur.com/8XpYIOI.png)

가운데 값인 5를 가지고  5보다 큰 값이 있는지 없는지 위아래로 확인을 합니다. 

왜 위아래로 확일은 하냐면 5가 중복된 데이터로 여러개가 존재할 수도 있기 때문입니다.
먼저 아래로 확인을 하면 3이기 때문에 5 아래의 값은 조회대상에서 제외가 됩니다.

그럼 이제 위쪽 부분에서 가운데를 고릅니다. 8이겠죠? 
그럼 8을 기준으로 확인을 합니다. 근데 `where a = 8`이기 때문에 `Member`테이블에 가서 