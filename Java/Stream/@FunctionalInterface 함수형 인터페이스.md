### 함수형 인터페이스란?
>단 하나의 추상 메서드만 가진 인터페이스를 말합니다. 이 덕분에 람다 표현식을 해당 인터페이스의 구현체로 사용할 수 있습니다. 
### **@FunctionalInterface 어노테이션:**  
>개발자가 해당 인터페이스가 함수형 인터페이스임을 명시하기 위해 사용할 수 있으며, 이 어노테이션은 실수로 추상 메서드를 추가하는 것을 방지해 줍니다.

>자바 8부터 도입된 함수형 프로그래밍 지원 기능에서는, **함수형 인터페이스**(Functional Interface)를 활용해 람다 표현식을 사용할 수 있게 되었습니다. 대표적인 함수형 인터페이스로는 **Consumer**, **Predicate**, **Function**, **Supplier** 등이 있습니다. 각각에 대해 자세히 살펴보면 다음과 같습니다.

---

## 2. 주요 함수형 인터페이스

### 2.1. Consumer
**역할:**  
>입력값을 받아서 특정 작업(주로 부수 효과, side-effect)을 수행하지만, 결과를 반환하지 않는 인터페이스입니다.

**핵심 메서드:**  
- `void accept(T t)`
- 전달받은 인자를 가지고 원하는 작업(예: 출력, 수정 등)을 수행합니다.

**예제:**
```java
Consumer<String> printer = s -> System.out.println(s);
printer.accept("Hello, Consumer!");
```

- **추가 메서드:**  
`andThen(Consumer<? super T> after)`를 통해 여러 Consumer를 순차적으로 실행할 수 있습니다.

---

### 2.2. Predicate
**역할:**  
>입력값을 받아서 조건을 평가하고 `boolean` 값을 반환하는 인터페이스입니다. 주로 필터링이나 조건 검증에 사용됩니다.

**핵심 메서드:**  
- `boolean test(T t)`
- 인자에 대해 조건을 검사하고, 조건을 만족하면 `true`, 그렇지 않으면 `false`를 반환합니다.

**예제:**
```java
Predicate<Integer> isEven = n -> n % 2 == 0;
System.out.println(isEven.test(4));  // true 출력
System.out.println(isEven.test(3));  // false 출력
```
- **추가 메서드:**  
`and()`, `or()`, `negate()` 등을 통해 복합 조건을 손쉽게 구성할 수 있습니다.


---

### 2.3. Function<T, R>
**역할:**  
>입력값(T)을 받아서 결과값(R)을 반환하는 함수형 인터페이스입니다. 주로 데이터를 변환하거나 매핑하는 데 사용됩니다.

**핵심 메서드:**  
- `R apply(T t)`
- 입력값을 받아서 원하는 연산을 수행한 후 결과값을 반환합니다.

**예제:**
```java
Function<String, Integer> stringLength = s -> s.length();
System.out.println(stringLength.apply("Hello"));  // 5 출력
```

- **추가 메서드:**  
`andThen(Function<? super R, ? extends V> after)`와 `compose(Function<? super V, ? extends T> before)`를 사용해 함수 연쇄 처리가 가능합니다.


---

### 2.4. Supplier
**역할:**  
>입력값 없이 결과값(T)을 공급하는 인터페이스입니다. 주로 객체 생성이나 데이터를 제공할 때 사용됩니다.

**핵심 메서드:**  
- `T get()`
- 인자 없이 실행되어 결과를 반환합니다.

**예제:**
```java
Supplier<Double> randomSupplier = () -> Math.random();
System.out.println(randomSupplier.get());  // 랜덤한 double 값 출력
```
---
### 1. UnaryOperator< T>

**정의:**  
>`UnaryOperator<T>`는 단일 인자를 받아 같은 타입의 결과를 반환하는 함수형 인터페이스입니다.  실제로는 `Function<T, T>`의 특수화된 형태입니다.

**용도:**
- 데이터 변환 또는 연산 시, 입력값을 가공하여 같은 타입의 결과를 얻고자 할 때 사용합니다.
- 예를 들어, 문자열을 대문자로 변환하거나 숫자에 일정한 연산(예: 제곱)을 수행할 때 유용합니다.
- **예제:**
```java
BinaryOperator<Integer> add = (a, b) -> a + b;
System.out.println(add.apply(3, 7));  // 결과: 10
```

---

### 2. BinaryOperator< T>

**정의:**  
>`BinaryOperator<T>`는 두 개의 동일한 타입의 인자를 받아 같은 타입의 결과를 반환하는 함수형 인터페이스입니다.  이는 `BiFunction<T, T, T>`의 특수화된 형태로 볼 수 있습니다.

**용도:**
- 두 개의 값을 조합하거나 연산할 때 사용합니다.
- 예를 들어, 두 숫자를 더하거나 문자열을 합치는 등의 연산에 적합합니다.
- **예제:**
```java
BinaryOperator<Integer> add = (a, b) -> a + b;
System.out.println(add.apply(3, 7));  // 결과: 10
```

---
## 3. 그 외 자주 사용되는 함수형 인터페이스
- **BiConsumer<T, U>:**  
>두 개의 입력값을 받아서 작업을 수행하며, 결과를 반환하지 않는 인터페이스입니다.

- **BiFunction<T, U, R>:**  
>두 개의 입력값을 받아서 하나의 결과값을 반환하는 인터페이스입니다.

---

## 4. 사용 시 주의점
- **불변성 유지:**  
>람다 표현식 내부에서 외부 변수를 사용할 경우, 해당 변수는 변경 불가능한(실제로는 "effectively final" 상태) 변수여야 합니다.

- **가독성:**  
>람다 표현식을 남용하면 오히려 가독성이 떨어질 수 있으므로, 간단한 로직이나 명확한 경우에 사용하는 것이 좋습니다.


---

이와 같이, 자바의 함수형 인터페이스는 람다 표현식과 함께 함수형 프로그래밍 패러다임을 지원하며, 코드의 간결성과 가독성을 크게 향상시킵니다. 각각의 인터페이스는 목적에 맞게 사용하면, 컬렉션 처리, 이벤트 처리, 데이터 변환 등 다양한 상황에서 효과적으로 활용할 수 있습니다.