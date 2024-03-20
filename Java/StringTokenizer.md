---
tags: java, StringTokenizer
---
```java
import java.util.StringTokenizer;

String input = br.readLine();
StringTokenizer st = null;
st = new StringTokenizer(input, " ");
st = new StringTokenizer(br.readLine());

int A = Integer.parseInt(st.nextToken());
java```

### StringTokenizer 클래스

`StringTokenizer` 클래스는 `java.util` 패키지에 포함되어 있으며, 문자열을 여러 토큰으로 분리하는 데 사용됩니다. 기본적으로 공백을 구분자로 사용하지만, 다른 문자를 구분자로 지정할 수도 있습니다. 

#### 생성자
1. **`StringTokenizer(String str)`**: 주어진 문자열 `str`을 공백 구분자를 사용하여 토큰으로 분리합니다.
2. **`StringTokenizer(String str, String delim)`**: 주어진 문자열 `str`을 지정된 구분자 `delim`을 사용하여 토큰으로 분리합니다.

#### 메서드
- **`hasMoreTokens()`**: 더 많은 토큰이 있으면 `true`를 반환합니다.
- **`nextToken()`**: 다음 토큰을 반환합니다.

#### 사용 예제
```java
StringTokenizer st = new StringTokenizer("Hello World");
while (st.hasMoreTokens()) {
    System.out.println(st.nextToken());
}
java```
