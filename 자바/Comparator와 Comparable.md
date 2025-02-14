---
상태: 진행중
tags:
  - 자바
시작일: 2025-02-14
마감일:
---
## Comparator와 Comparable
> 객체 정렬에 필요한 메서드(정렬기준 제공)를 정의한 인터페이스

**Comparator** : 기본 정렬기준 외에 **다른 기준으로 정렬하고자 할 때** 사용
**Comparable** : **기본 정렬기준**을 구현하는데 사용.

```java
public interface Comparator {
	int compare (Object o1, Object o2); // o1, o2 두 객체를 비교
	boolean equals (Object obj); // equals를 오버라이딩하라는 뜻
}

public interface Comparable {
	int compareTo (Object o); // 주어진 객체 (o)를 자신과 비교
	
}
```

- compare()와 compareTo()는 두 객체의 비교결과를 반환하도록 작성
```java
public final class Integer extends Number implements Comparable {
	public int compareTo(Integer anotherInteger) {
		int v1 = this.value;
		int v2 = anotherInteger.value;
		// 같으면0, 오른쪽 값이 크면 -1, 작으면 1을 반환
		return (v1 < v2 ? -1 : (v1==v2 ? 0 : 1));
	}
}
```