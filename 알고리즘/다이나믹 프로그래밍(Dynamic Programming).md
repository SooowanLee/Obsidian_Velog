---
상태: 진행중
tags:
  - 알고리즘
시작일: 2025-02-14
마감일:
---
## 다이나믹 프로그래밍
>큰 문제를 작은 문제로 나누어 해결하고, 그 결과를 저장하여 동일한 작은 문제가 다시 등장했을 때 재계산하지 않고 저장된 값을 재사용하는 방식

### 아래의 조건을 충족해야 다이나믹 프로그래밍을 사용할 수 있다.
#### 🔥핵심 개념 : 부분 문제(Overlapping Subproblems) + 최적 부분 구조(Optimal Substructure)
- **부분 문제** : 큰 문제를 작은 문제로 나누었을 때, 동일한 작은 문제가 여러 번 반복해서 나타나는 경우
- **최적 부분 구조** : 문제의 최적 해결 방법이 그 하위 문제들의 최적 해결 방법을 조합하여 만들 수 있는 경우

### DP 해결 방식
- **Top-Down** (메모이제이션, Memoization)
	- **재귀(Recursion) + 캐싱**
	- 큰 문제를 작은 문제로 쪼개서 **재귀적으로** 해결하며, 이미 해결한 작은 문제의 결과를 저장하여 중복 계산을 방지
- **Bottom-up** (탭 메모이제이션, Tabulation)
	- 작은 문제부터 차례로 풀어나가며 **테이블(배열)에 결과를 저장**
	- 재귀 호출을 사용하지 않고 반복문을 활용하여 성능이 더욱 향상됨

### DP를 사용하는 이유 (vs. 단순 재귀)
#### ❌ 일반적인 재귀 방식의 문제점
단순 재귀는 같은 부분 문제가 여러 번 반복적으로 호출되어 비효율적입니다.
예제: 피보나치 수열 (일반 재귀)
```java
public class Fibonacci {
    public static int fib(int n) {
        if (n <= 1) return n;
        return fib(n - 1) + fib(n - 2);
    }

    public static void main(String[] args) {
        System.out.println(fib(10)); // 55
    }
}

```
✅**시간 복잡도: O(2^n)** → 너무 느림 (중복 계산 발생)

###  DP를 활용한 개선 방법
#### 1. Top-Down 방식 (메모이제이션)
```java
import java.util.*;

public class Fibonacci {
    static Map<Integer, Integer> memo = new HashMap<>();

    public static int fib(int n) {
        if (n <= 1) return n;
        if (memo.containsKey(n)) return memo.get(n);

        int result = fib(n - 1) + fib(n - 2);
        memo.put(n, result);
        return result;
    }

    public static void main(String[] args) {
        System.out.println(fib(10)); // 55
    }
}

```