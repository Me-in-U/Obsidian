---
tags: 피보나치, java, math, matrux
---
# 피보나치 수열 계산: 행렬 방법
피보나치 수열의 n번째 항을 계산하는 데 행렬 방법을 사용하는 이유와 해당 자바 코드에 대해 설명하겠습니다.

## 행렬 방법의 이점
행렬 방법을 사용하는 주된 이유는 계산 속도를 획기적으로 향상시킬 수 있기 때문입니다. 특히, 큰 n에 대한 피보나치 수를 계산할 때 유용합니다. 이 방법의 이점은 다음과 같습니다:

1. **효율적인 거듭제곱 계산**: 행렬을 사용하면 피보나치 수열을 거듭제곱 형태로 표현할 수 있으며, <mark style="background: #FF5582A6;">O(log n) 시간 복잡도</mark>로 피보나치 수를 계산할 수 있습니다. 이는 단순 재귀나 반복을 사용한 O(n) 시간 복잡도에 비해 훨씬 빠릅니다.
2. **메모리 효율성**: 행렬 방법은 필요한 메모리 양을 줄여줍니다. 단순 재귀 방법은 중복 계산이 많아 메모리 사용이 비효율적입니다.
3. **큰 수에 대한 빠른 계산**: n이 매우 클 때, 행렬 방법은 계산을 빠르게 수행할 수 있습니다. 단순 반복 방법을 사용하면, 이러한 큰 수에 대한 계산은 실용적이지 않습니다.

## 행렬 방법의 작동 방식

1. 피보나치 수열은 선형 동차 점화식으로 표현됩니다: 
F(n) = F(n-1) + F(n-2)

1. 이 점화식은 행렬 형태로 다음과 같이 표현할 수 있습니다:
F(0)=0, F(1)=1

| F(n)    |      | 1 1 |     | F(n-1) |
|            |  =  |      |  *  |            |
| F(n-1) |      | 1 0 |     | F(n-2) |

| F(n+1)|      | 1 1 |      | F(n)   |
|            |  =  |      |  *  |           |
| F(n)    |      | 1 0 |     | F(n-1) |
(행렬 곱)


3. 이 행렬을 n-1번 곱하면, n번째 피보나치 수를 얻을 수 있습니다. 이 과정을 빠르게 수행하기 위해 거듭제곱 분할을 사용합니다.

## 코드
자바 코드는 위에서 설명한 행렬 방법을 구현하여 n번째 피보나치 수를 계산하고, 그 결과를 1,000,000,007로 나눈 나머지를 반환합니다. 코드는 `Fibonacci` 클래스에 정의되며, `fibonacci` 메서드와 `multiplyMatrix` 메서드를 포함합니다.

- `fibonacci` 메서드: n번째 피보나치 수를 계산합니다.
- `multiplyMatrix` 메서드: 두 개의 2x2 행렬을 곱하고 결과를 반환합니다.
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
  static final long MOD = 1000000007L;  

  public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    long n = Long.parseLong(br.readLine());
    System.out.println(fibonacci(n));
  }

  public static long fibonacci(long n) {
    if (n <= 1)
      return n; 

    long[][] result = { // 단위 행렬
        { 1, 0 },
        { 0, 1 }
    };
    long[][] fiboM = { // 피보나치 행렬
        { 1, 1 },
        { 1, 0 }
    };
	//n이 짝수라면, x^n은 (x^(n/2)) * (x^(n/2))
	//n이 홀수라면, x^n은 x * (x^(n-1))

	//n이 짝수인 경우: 행렬을 제곱하고 거듭제곱 값을 반으로 줄입니다:
	//fiboM^n = fiboM^(n/2) * fiboM^(n/2)
    
	//n이 홀수인 경우: 먼저 result 행렬을 fiboM으로 곱한 다음 행렬을 제곱하고 거듭제곱 값을 줄입니다: 
	//fiboM^n = result * fiboM * fiboM^(n-1).
    while (n > 0) {
      if (n % 2 == 1) { //n이 홀수라면
        result = multiplyMatrix(result, fiboM);
      }
      n /= 2;   
      fiboM = multiplyMatrix(fiboM, fiboM); // 행렬 
    }
    return result[1][0];
  }  

  public static long[][] multiplyMatrix(long[][] a, long[][] b) {
    long[][] result = new long[2][2];
    for (int i = 0; i < 2; i++) {
      for (int j = 0; j < 2; j++) {
        result[i][j] = 0;
        for (int k = 0; k < 2; k++) {
          result[i][j] = (result[i][j] + (a[i][k] * b[k][j])) % MOD;
        }
      }
    }
    return result;
  }
}
```

## 결론
행렬 방법은 피보나치 수열을 빠르고 효율적으로 계산하는 데 매우 유용합니다. 이 방법은 n이 매우 클 때도 빠르게 작동하며, 메모리 사용이 효율적입니다.
