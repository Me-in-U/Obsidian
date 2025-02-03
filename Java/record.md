---
tags: java, record
---
코들린의 Data 클래스와 같은 데이터을 위한 클래스이다.

이전 자바에서는 DTO 클래스를 만들 경우 getter, setter , construcotr 등 직접 작성하거나 3rd party 라이브러리인 lombok 을 이용할 수 있었다. 하지만 Java 14 에 와서 record 라는 새로운 structure 추가됐고 이를 이용해 코틀린 처럼 DTO 클래스를 쉽게 만들 수 있다. 

```java
public static void main(String[] args) {
    createMember();
}

public static void createMember() {
    var m  = new Member("marco", 30);
    System.out.println(m);
    System.out.println("Age=" + m.age());
    System.out.println("Name=" + m.name());
    //출력
    /*
    Member[name=marco, age=30]
	Age=30
	Name=marco
    */
}

public static record Member(String name, int age) {
    public Member(int age) {
        this("Anonymous", age);
    }
}
```