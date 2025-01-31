---
tags: java, static, dynamic, binding
---
### 1. **정적 바인딩 (Static Binding)**
- **정의**: 컴파일 시점에 메서드 호출이 결정되는 바인딩.
- **특징**:
    1. **컴파일 시점**에 바인딩이 이루어짐.
    2. 주로 `static`, `private`, `final` 메서드 또는 **오버로딩**된 메서드에서 사용됨.
    3. 메서드 호출 시점에 **클래스 타입**을 기준으로 호출할 메서드가 결정됨.
    4. 빠른 실행 속도(런타임 검사 없음).
- **사용 예제**:
```java
class Parent {
    private void privateMethod() {
        System.out.println("Parent's privateMethod");
    }

    static void staticMethod() {
        System.out.println("Parent's staticMethod");
    }

    final void finalMethod() {
        System.out.println("Parent's finalMethod");
    }
}

class Child extends Parent {
    // static, private, final 메서드는 오버라이딩되지 않음
    static void staticMethod() {
        System.out.println("Child's staticMethod");
    }
}

public class Main {
    public static void main(String[] args) {
        Parent p = new Child();

        // 정적 바인딩
        Parent.staticMethod(); // Parent's staticMethod
        Child.staticMethod();  // Child's staticMethod
    }
}

```

### 2. **동적 바인딩 (Dynamic Binding)**
- **정의**: 런타임 시점에 메서드 호출이 결정되는 바인딩.
- **특징**:
    1. **런타임 시점**에 바인딩이 이루어짐.
    2. 메서드 오버라이딩을 통해 다형성을 지원.
    3. 메서드 호출 시점에 **객체의 실제 타입**을 기준으로 호출할 메서드가 결정됨.
    4. 오버라이딩된 메서드는 항상 동적 바인딩됨.
- **사용 예제**:
```java
class Parent {
    void method() {
        System.out.println("Parent's method");
    }
}

class Child extends Parent {
    @Override
    void method() {
        System.out.println("Child's method");
    }
}

public class Main {
    public static void main(String[] args) {
        Parent p = new Child();

        // 동적 바인딩
        p.method(); // Child's method
    }
}
```

### **4. 혼합 사용 예제** 
```java
class Parent {
	static String a = "Parent's static field";
	
    static void staticMethod() {
        System.out.println("Parent's staticMethod");
    }

    void instanceMethod() {
        System.out.println("Parent's instanceMethod");
    }
}

class Child extends Parent {
	static String a = "Child's static field";

    static void staticMethod() {
        System.out.println("Child's staticMethod");
    }

    @Override
    void instanceMethod() {
        System.out.println("Child's instanceMethod");
    }
}

public class Main {
    public static void main(String[] args) {
        Parent p = new Child();

		// 정적 필드 
		System.out.println("Static field: " + p.a); // Parent's static field (정적 바인딩)

        // 정적 바인딩
        p.staticMethod(); // Parent's staticMethod (클래스 타입 기준)

		// 인스턴스 필드
		System.out.println("Instance field: " + ((Child) p).instanceField); // Child's instance field
		
        // 동적 바인딩
        p.instanceMethod(); // Child's instanceMethod (객체 타입 기준)
    }
}
```
- `staticMethod()`는 클래스 타입(`Parent`) 기준으로 정적 바인딩됨.
- `instanceMethod()`는 객체 타입(`Child`) 기준으로 동적 바인딩됨.