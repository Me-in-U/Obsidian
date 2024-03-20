```java
private static void oldStyle() {
    String text = "{\n" +
                  "  \"name\": \"John Doe\",\n" +
                  "  \"age\": 45,\n" +
                  "  \"address\": \"Doe Street, 23, Java Town\"\n" +
                  "}";
    System.out.println(text);
}
```
->
```java
private static void jsonMovedBracketsBlock() {
    String text = """
            {
                "name": "John Doe",
                "age": 45,
                "address": "Doe Street, 23, Java Town"
            }
            """; // 이 라인 space 공백 2개 제거하여 왼쪽으로 이동
    System.out.println(text);
}
```