---
tags: java, BigInteger, 큰수
---
```java
import java.math.BigInteger;

// 16진법
BigInteger bigIntWithRadix = new BigInteger("64", 16);
// 정수로 생성
BigInteger bigIntWithValue = BigInteger.valueOf(100);
// 문자열
BigInteger bigIntWithString = new BigInteger("100");

//--------------------BigInteger 계산---------------------
System.out.println("덧셈(+) :" +bigNumber1.add(bigNumber2));
System.out.println("뺄셈(-) :" +bigNumber1.subtract(bigNumber2));
System.out.println("곱셈(*) :" +bigNumber1.multiply(bigNumber2));
System.out.println("나눗셈(/) :" +bigNumber1.divide(bigNumber2));
System.out.println("나머지(%) :" +bigNumber1.remainder(bigNumber2));

//--------------------BigInteger 형 변환---------------------
int int_bigNum = bigNumber.intValue(); //BigIntger -> int
long long_bigNum = bigNumber.longValue(); //BigIntger -> long
float float_bigNum = bigNumber.floatValue(); //BigIntger -> float
double double_bigNum = bigNumber.doubleValue(); //BigIntger -> double
String String_bigNum = bigNumber.toString(); //BigIntger -> String

//--------------------BigIntger 두 수 비교---------------------
int compare = bigNumber1.compareTo(bigNumber2);
System.out.println(compare);
```

```java
package P14928_큰_수_(Big)

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

class Main {
  public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    String input = br.readLine();
    int divider = 20000303;
    int result = 0;
    for(int i = 0; i < input.length(); i++){
      result = (result * 10 + (input.charAt(i) - '0')) % divider;
    }
    
    System.out.println(result);
  }
}
```