---
상태: 완료
tags:
  - 자료구조
시작일: 2025-01-09
마감일: 2025-01-09
---
## **Set**
- 중복 허용 X
- 순서 보장 X(순서를 보장하는 경우도 있음)

### Set은 ADT(Abstract Data Type)이다 
Set은 Interface이고 Set을 구현한 구현체인 HashSet, SortedSet등이 있다.

## **HashSet**
HashSet의 구현체는 HashMap이다.

HashMap은 key:value로 테이블 형태로 데이터를 저장
key는 중복X, value는 중복 O

HashSet에서 사용하는 HashMap은 Key만 사용하고 Value부분에는 그냥 0,1 같은 dummy 값을 넣는다.

## **HashMap**
key:value로 데이터를 저장

### 특징
**삽입, 삭제, 갱신, 탐색이 O(1)(상수)시간에 처리된다.** 
상수시간으로 데이터가 처리된다는 것은 아무리 데이터가 커지더라도 일정 시간안에 데이터를 처리 가능하다.
반대로, O(n)만큼의 시간이 걸리는 자료구조는 데이터의 사이즈가 커질수록 비례해서 시간이 늘어난다.

### 예) 인기투표: 한국의 영화배우
투표 참여자 : 전국민 5,500만명 / 한 명씩 자신이 좋아하는 영화배우에게 투표한다.
![](https://i.imgur.com/dI3HOEh.png)

List를 사용해서 미리 배우 이름을 넣어두기에는 배우가 너무 많다.
HashMap을 사용해서 배우 이름이 나올 때 마다 key에 저장을 하고 똑같은 배우가 나온다면 value++하면 효율적으로 투표가 가능하다.

### HashMap(=Hash Table)
- 배열의 특징인 상수시간으로 처리하는 기능을 사용해서 구현
- 하나의 key는 하나의 value에 맵핑
- value는 배열의 index에 저장
- HashFunction 함수를 사용해서 key를 배열의 index로 변환
- key는 중복X


#### 내부 구현
- 배열(Array)을 사용하여 구현
- 배열에 저장하기 위해 key의 hash를 구해야함
- hash function으로 key의 hash를 구함
- 구해진 hash를 배열 사이즈로 modular(%) 한 값을 index로 사용
#### HashFunction이 중요하다!
충돌 가능성에 영향을 준다.

#### 해시 충돌(Hash Collision)
서로 다른 key들이 같은 hash를 가질 때 발생
**key1 != key2 BUT!!! hf(key1) == hf(key2)**

HashMap에서 또 다른 의미의 해시 충돌
**hf(key1) != hf(key2) BUT!!! hf(key1) % M == hf(key2) % M**