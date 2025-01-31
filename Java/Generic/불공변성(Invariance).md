---
tags: invariance, java, generic, wildcard
---
```java
GenericBox<Object> oBox = new GenericBox<>();
GenericBox<String> sBox = oBox; // ❌ 컴파일 에러 발생
```
#### **📌 컴파일 에러 발생 이유**

- `GenericBox<Object>` **(Object 타입을 받는 제네릭 박스)** 와 `GenericBox<String>` **(String 타입을 받는 제네릭 박스)** 는 **다른 타입**으로 취급됩니다.
- 즉, `GenericBox<Object>`는 `GenericBox<String>`의 부모 타입이 **아님**. 따라서 **서로 대입할 수 없음**.

#### **🔍 제네릭의 불공변성(Invariance)**

- 자바의 제네릭은 기본적으로 **불공변(invariant)** 하기 때문에,  
    `GenericBox<Object>`가 `GenericBox<String>`의 부모 클래스가 아닙니다.
- 즉, `GenericBox<T>`에서 `T`가 다르면 서로 **호환되지 않음**.
#### **📌 해결 방법**

##### **1. 와일드카드(?) 사용**
```java
GenericBox<?> box = oBox;  // ✅ 가능 (비한정 와일드카드)
```
- `GenericBox<?>`는 **모든 타입의 GenericBox를 참조 가능**하므로, 위 코드는 정상적으로 컴파일됩니다.

##### **2. 제네릭 타입 경계를 설정**
```java
GenericBox<? extends Object> box = oBox;  // ✅ 가능
```
- `? extends Object`는 `Object`를 포함한 모든 하위 타입을 받을 수 있습니다.