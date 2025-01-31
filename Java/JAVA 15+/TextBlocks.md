---
tags: java, textblock
---
- **Java 13**: Text Block이 **미리 보기 기능**으로 도입.
- **Java 14**: 여전히 **미리 보기 기능**으로 제공.
- **Java 15**: Text Block이 **정식 기능**으로 추가.
```java
public static void main(String[] args) {
    System.out.println(greeting("무명소졸"));
    //print Hello 무명소졸
}

public static String greeting(String name) {
    return """
        Hello %s
        """.formatted(name);
}
```