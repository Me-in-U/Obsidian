---
tags: java, format, formatter
---
```java
public static String repeat(String str, int times) {
	return String.format("%0" + times + "d", 0).replace("0", str);
}
```

### 1. String 클래스의 format 메서드

`String` 클래스의 `format` 메서드는 정적 메서드로, 문자열을 특정 형식에 맞게 포매팅하는데 사용됩니다. 메서드의 시그니처는 다음과 같습니다:

javaCopy code
```java
public static String format(String format, Object... args)
```

- **format**: 형식 문자열. 여기에는 텍스트와 함께 형식 지정자(예: `%s`, `%d` 등)가 포함됩니다.
- **args**: 형식 지정자에 대응하는 인수들. 가변 인수를 사용하여 여러 인수를 전달할 수 있습니다.

예제:
```java
String result = String.format("Hello, %s! You are %d years old.", "John", 30); System.out.println(result); // 출력: Hello, John! You are 30 years old.
```

### 2. Formatter 클래스

`Formatter` 클래스는 더 복잡한 문자열 포매팅 작업을 수행할 수 있는 클래스입니다. `Formatter` 인스턴스를 생성하고, `format` 메서드를 사용하여 문자열을 포매팅할 수 있습니다.

예제:
```java
Formatter formatter = new Formatter(); 
formatter.format("Pi is approximately %f", Math.PI); System.out.println(formatter.toString()); // 출력: Pi is approximately 3.141593
```

이러한 `format` 메서드들은 다양한 형식 지정자를 사용하여 문자열, 숫자, 날짜 등을 다양한 형식으로 포매팅할 수 있습니다.