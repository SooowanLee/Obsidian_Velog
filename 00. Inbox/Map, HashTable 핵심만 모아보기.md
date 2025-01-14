---
상태: 진행중
tags:
  - 자료구조
시작일: 2025-01-14
마감일:
---
## Map
> Key-Value 로 데이터를 저장하는 ADT(추상 자료형)
> key는 중복될 수 없다.
> associative array, dictionary라고 불리기도 한다.

### Hash Table(Hash Map)
배열과 해시 함수(hash function)를 사용하여 map을 구현한 자료 구조
(일반적으로) 상수 시간으로 데이터에 접근하기 때문에 매우 빠르다.

### Hash Function
임의의 크기를 가지는 type의 데이터를 고정된 크기를 가지는 type의 데이터롤 변환하는 함수
(hash table에서)임의의 데이터를 정수로 변환하는 함수

예를 들어)  **"김철수"** 라는 이름을 **hash function** 