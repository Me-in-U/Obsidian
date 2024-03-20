---
tags: java, math, mod, exponent
---
(A + B) mod M = ((A mod M) + (B mod M)) mod M
(A *  B) mod M = ((A mod M) *  (B mod M)) mod M

![[mod1.png]]
![[mod2.png]]
![[mod3.png]]

```java
// A = 밑, exponent = 지수
long pow(long A, long exponent) {

	// 지수가 1일 경우 A^1 이므로 A를 그대로 리턴
	if(exponent == 1) {
		return A % C;
	}

	// 지수의 절반에 해당하는 A^(exponent / 2) 을 구한다.
	long temp = pow(A, exponent / 2);

	/*
	 * 현재 지수가 "홀수" 였다면
	 * A^(exponent / 2) * A^(exponent / 2) * A 이므로
	 * A를 한 번 더 곱해주어야 한다.
	 *
	 * ex) A^9 = A^4 * A^4 * A
	 */
	if(exponent % 2 == 1) {
		return (temp * temp % C) * A % C;
	}else{
		// 그 외에는 "짝수"이므로 구했던 값을 한 번 더 곱해서 반환한다.
		return temp * temp % C;
	}
}
```

![[mod4.png]]
```java
// (a * b) % C = ((a % C)*(b % C)) % C
(temp * temp * A) % C = ((temp * temp % C)     * (A % C)) % C
					= (((temp * temp % C) % C) * (A % C)) % C
					=  ((temp * temp % C) * A) % C
```

```java
if(exponent % 2 == 1) {
	return temp * temp * A % C;
}//잘못된 식
```

문제에서 주어지는 각 최댓값은 int형의 max값이다. 즉, 2,147,483,647 (231-1)을 입력받을 수 있다는 뜻이다. 대략 2*109 정도 된다.

long형의 경우 9,223,372,036,854,775,807 (263-1) 이고 대략 9*1018 정도 된다.

예로들어 temp가 2,147,483,647 라면 어떻게 할 것인가.

temp * temp는 long형 안에서 오버플로우 없이(long 타입 범위 안) 가능하다. (231-1) * (231-1) < 263-1 이 식을 만족하기 때문에

temp * temp % C는 가능하다는 뜻이다.

하지만, 밑 또한 2,147,483,647 이라면 어떻게 될까?

(2^31-1) * (2^31-1) * (2^31-1) ≒ 294 로 딱 보더라도 long 형 범위를 넘어간다.

즉, temp * temp * A % C 에서 **temp * temp * A 이 부분이 long 범위를 넘어가면서 잘못된 값으로 계산이 되어버린다.**