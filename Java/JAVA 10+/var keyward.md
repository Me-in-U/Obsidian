---
tags: java, var
---
가변형 변수 type 이다. 동적 타이핑 되는 python, 코틀린과 같은 언어에서 사용되고 있으면 java 에서도 도입했다.
멤버 변수로는 사용할 수 없으면 지역 스코프에서만 사용 가능하다. 
```java
public void sayHello() {
    var greeting = "Hello world!";
    System.out.println(greeting);
}
```
