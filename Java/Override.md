---
tags: java, override, method, Polymorphism
---
## 오버라이딩의 조건
- **메서드 이름이 같아야 한다.**
    - 부모 클래스와 동일한 메서드 이름을 가져야 오버라이딩으로 인식됩니다.
- **매개변수의 개수, 타입, 순서가 같아야 한다.**
    - 부모 메서드의 시그니처를 정확히 동일하게 정의해야 합니다.
    - 매개변수가 다르면 **오버로딩(Overloading)**이 됩니다.
- **리턴 타입이 같아야 한다.**
    - 자바 5부터는 **공변 반환 타입(Covariant Return Type)**을 지원하여, 리턴 타입이 부모 메서드의 리턴 타입이거나 그 하위 타입이면 가능합니다.
- **접근 제한자는 부모보다 범위가 넓거나 같아야 한다.**
    - 예를 들어, 부모 메서드가 `protected`라면 오버라이딩된 메서드는 `protected` 또는 `public`이어야 하며, `private`으로는 변경할 수 없습니다.
- **조상보다 더 큰 예외를 던질 수 없다.**
    - 부모 메서드가 던지는 예외(Exception)보다 같은 범위거나 더 구체적인 예외만 던질 수 있습니다.
    - 부모 메서드가 예외를 던지지 않는 경우, 오버라이딩 메서드도 예외를 던지면 안 됩니다

- **어노테이션 사용:**  
    오버라이딩할 때는 `@Override` 어노테이션을 사용하는 것이 권장됩니다. 이는 컴파일러가 오버라이딩 규칙을 준수하는지 검사하도록 도와줍니다.
    
- **다형성(Polymorphism):**  
    오버라이딩된 메서드는 런타임 시 동적 바인딩(Dynamic Binding)을 통해 호출됩니다. 즉, 부모 클래스 타입의 참조 변수로 자식 클래스 객체를 참조할 경우, 자식 클래스의 오버라이딩 메서드가 실행됩니다.


```java
class Parent {
    protected String greet(String name) throws Exception {
        return "Hello, " + name;
    }
}

class Child extends Parent {
    // 오버라이딩된 메서드
    @Override
    public String greet(String name) {
        return "Hi, " + name;
    }
}

public class Main {
    public static void main(String[] args) {
        Parent parent = new Parent();
        Parent child = new Child();

        try {
            System.out.println(parent.greet("Parent")); // "Hello, Parent"
            System.out.println(child.greet("Child"));   // "Hi, Child"
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### **중요 포인트**

- **접근 제한자 확장:**
```java
protected → public (가능)
protected → private (불가능)
```
- **예외 범위 제한:**
```java
class Parent {
    void method() throws IOException {}
}
class Child extends Parent {
    // 더 구체적인 예외는 허용
    @Override
    void method() throws FileNotFoundException {}
}
```
- **공변 반환 타입 예시:**
```java
class Parent {
    Object getValue() { return "Parent"; }
}

class Child extends Parent {
    @Override
    String getValue() { return "Child"; }
}

```