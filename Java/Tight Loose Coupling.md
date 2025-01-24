### **Tight Coupling (강한 결합)**

클래스나 모듈 간 의존성이 높아져 서로 밀접하게 연결된 상태를 의미합니다. 하나의 변경이 다른 클래스나 모듈에 영향을 미치기 쉬운 구조입니다.

#### **특징**

1. **의존성 증가**:
    - 클래스 A가 클래스 B의 구체적인 구현에 의존합니다.
    - A를 변경하면 B도 수정해야 할 가능성이 높습니다.
2. **유지보수 어려움**:
    - 코드 수정 시 많은 부분에 영향을 줄 수 있어 수정이 어렵고 버그가 발생할 가능성이 큽니다.
3. **확장성 부족**:
    - 새로운 요구사항이나 기능 추가가 어렵습니다.

#### **예시**
```java
// 강한 결합: PaymentService가 CreditCardProcessor에 의존
public class PaymentService {
    private CreditCardProcessor processor = new CreditCardProcessor(); // 특정 클래스 직접 의존

    public void makePayment(double amount) {
        processor.processPayment(amount); // 변경 어려움
    }
}

class CreditCardProcessor {
    public void processPayment(double amount) {
        System.out.println("Processing payment: " + amount);
    }
}

```

- `PaymentService`는 `CreditCardProcessor`의 구체적인 클래스에 의존하므로 다른 결제 프로세서를 사용하려면 코드를 수정해야 함.

---

### **Loose Coupling (느슨한 결합)**

클래스나 모듈 간 의존성이 낮고 상호작용이 인터페이스나 추상화 계층을 통해 이루어지는 상태를 의미합니다. 변경에 유연하며 독립성이 높습니다.

#### **특징**

1. **의존성 감소**:
    - 클래스 A는 클래스 B의 구체적인 구현이 아닌 인터페이스나 추상 클래스에 의존합니다.
    - 변경이 발생해도 영향을 최소화할 수 있습니다.
2. **유지보수 용이**:
    - 코드를 쉽게 수정하거나 교체할 수 있습니다.
3. **확장성 증가**:
    - 새로운 클래스나 기능을 추가할 때 기존 코드를 거의 수정하지 않아도 됩니다.

#### **예시**
```java
// 느슨한 결합: PaymentService가 PaymentProcessor 인터페이스에 의존
public interface PaymentProcessor {
    void processPayment(double amount);
}

public class CreditCardProcessor implements PaymentProcessor {
    public void processPayment(double amount) {
        System.out.println("Processing credit card payment: " + amount);
    }
}

public class PayPalProcessor implements PaymentProcessor {
    public void processPayment(double amount) {
        System.out.println("Processing PayPal payment: " + amount);
    }
}

public class PaymentService {
    private PaymentProcessor processor; // 인터페이스 의존

    public PaymentService(PaymentProcessor processor) {
        this.processor = processor;
    }

    public void makePayment(double amount) {
        processor.processPayment(amount); // 교체 가능
    }
}

// 사용
public class Main {
    public static void main(String[] args) {
        PaymentProcessor processor = new CreditCardProcessor(); // 구현체 교체 가능
        PaymentService service = new PaymentService(processor);
        service.makePayment(100.0);

        processor = new PayPalProcessor(); // 다른 구현체로 변경
        service = new PaymentService(processor);
        service.makePayment(200.0);
    }
}

```
- `PaymentService`는 `PaymentProcessor` 인터페이스에만 의존하므로 구현체를 자유롭게 변경 가능.

---

### **Tight Coupling vs Loose Coupling 비교**

|**특성**|**Tight Coupling**|**Loose Coupling**|
|---|---|---|
|**의존성**|구체적인 클래스에 의존|인터페이스나 추상 클래스에 의존|
|**변경의 영향**|변경이 다른 모듈에 큰 영향을 미침|변경이 제한된 부분에만 영향을 미침|
|**유지보수**|복잡하고 어려움|쉬움|
|**확장성**|새로운 요구사항 추가가 어려움|기능 추가와 확장이 용이|
|**재사용성**|낮음|높음|

---

### **Loose Coupling을 구현하는 방법**

1. **인터페이스나 추상 클래스 사용**:
    - 클래스 간의 직접적인 연결을 끊고 추상화를 통해 간접적으로 연결.
2. **의존성 주입(Dependency Injection)**:
    - 객체를 생성자, 메서드, 또는 필드를 통해 외부에서 주입.
3. **팩토리 패턴 사용**:
    - 객체 생성을 팩토리 클래스를 통해 처리하여 결합도를 줄임.
4. **이벤트 기반 구조**:
    - 이벤트 핸들러를 통해 모듈 간의 간접적인 상호작용을 지원.