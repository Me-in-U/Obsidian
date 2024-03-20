---
tags:
  - java
  - 피보나치
  - dp
  - match
---
동적 프로그래밍은 재귀 방법의 중복 계산 문제를 해결하기 위한 방법입니다. 이 방법에서는 한 번 계산된 피보나치 수를 메모리에 저장하고, 이후 같은 피보나치 수를 계산할 때 이전에 저장된 값을 재사용합니다. 이를 메모이제이션이라고 합니다. 
### 코드
```java
public static long fibonacci(int n) {
    long[] memo = new long[n + 1];
    memo[1] = 1;
    memo[2] = 1;
    for (int i = 3; i <= n; i++) {
        memo[i] = memo[i - 1] + memo[i - 2];
    }
    return memo[n];
}
```
```java
public static long fibonacci(int n) {
	if (memo == null) 
		memo = new long[n + 1];        
	if (n <= 2)
		return 1;        
	if (memo[n] != 0) 
		return memo[n];        
	memo[n] = fibonacci(n - 1) + fibonacci(n - 2);
	return memo[n];
}
```

1. **메모 배열 초기화**: `n+1` 길이의 `memo` 배열을 생성하여 0번째와 1번째 피보나치 수를 초기화합니다.

2. **반복문을 통한 계산**: 2부터 n까지의 피보나치 수를 계산하며, 각 피보나치 수는 이전 두 피보나치 수의 합으로 계산됩니다. 계산된 피보나치 수는 `memo` 배열에 저장됩니다.

3. **결과 반환**: `memo[n]`을 반환하여 n번째 피보나치 수를 얻습니다.

### 장단점
- **장점**: 중복 계산이 없으므로 <mark style="background: #FF5582A6;">시간 복잡도가 O(n)</mark>입니다. 이는 재귀 방법에 비해 훨씬 효율적입니다.
- **단점**: 메모리 사용량이 증가합니다. n까지의 모든 피보나치 수를 저장해야 하므로 <mark style="background: #FF5582A6;">공간 복잡도가 O(n)</mark>입니다.