---
tags: java, math, GCD, 최소공배수, 최소공약수, 기약분수
---
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;
import java.util.StringTokenizer;

public class Main {
  public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    StringBuilder sb = new StringBuilder();
    StringTokenizer st = null;

    int N = Integer.parseInt(br.readLine());
    for (int i = 0; i < N; i++) {
      st = new StringTokenizer(br.readLine());
      int a = Integer.parseInt(st.nextToken());
      int b = Integer.parseInt(st.nextToken());
      int d = gcd(a, b);
      sb.append(a * b / d).append('\\n');
    }
    System.out.print(sb);
  }

  // 최대공약수 반복문 방식
  public static int gcd(int a, int b) {
    while (b != 0) {
      int r = a % b; // 나머지를 구해준다.
      // GCD(a, b) = GCD(b, r)이므로 변환한다.
      a = b;
      b = r;
    }
    return a;
  }
}
```

반복문
``` java
public static int gcd(int a, int b) {
  int r1 = a;
  int r2 = b;
  while(r2 > 0) {
	  int q = r1 / r2;
	  int r = r1 - (q * r2);
	  int r1 = r2;
	  int r2 = r;
  }
}
```

유클리드 호재법
```java
public static int getGCD(int a, int b) {
	if(b==0) {
		return a;
	}
	return getGCD(b, a%b);
}
```

기약분수
```JAVA
int 분자 = a;
int 분모 = b;

int gcd = getGCD(a,b);

System.out.println((a/gcd) + "/" + (b/gcd));
```