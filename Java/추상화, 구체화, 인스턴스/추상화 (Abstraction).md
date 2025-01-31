---
tags: java, abstraction
---
### **1. 추상화 (Abstraction)**

#### **정의**

- **필요한 정보만 남기고 불필요한 세부 사항을 제거하는 과정**.
- 복잡한 시스템에서 **핵심적인 속성과 동작만을 정의**하여 사용자가 더 쉽게 이해하고 사용할 수 있도록 합니다.

#### **특징**

- 객체 지향 프로그래밍에서 **클래스를 설계**할 때 사용하는 개념.
- 현실 세계의 사물이나 개념을 **프로그래밍의 클래스나 인터페이스로 표현**.

#### **예제**

```java
abstract class Animal {
    abstract void sound(); // 소리 내기 (공통된 동작 정의)
}
class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("멍멍");
    }
}
class Cat extends Animal {
    @Override
    void sound() {
        System.out.println("야옹");
    }
}

```

- **추상화**: `Animal` 클래스는 동물이라는 공통 개념을 정의하고, **세부 구현은 각 동물(Dog, Cat)이 책임**.
- `Animal`은 "동물"이라는 큰 개념을 추상화하고, 세부 구현은 **구체화** 단계에서 이루어집니다.