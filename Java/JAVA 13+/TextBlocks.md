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