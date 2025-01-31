---
tags: java, interface
---
## 인터페이스의 필요성
1. **구현의 강제화 및 표준화**
    - 인터페이스는 클래스 설계에서 반드시 구현해야 할 메서드의 목록을 제공하여 일관성과 표준화를 강제합니다.
    - `abstract` 메서드를 통해 인터페이스를 상속받는 클래스는 반드시 정의된 메서드를 구현해야 합니다.
2. **모듈 교체의 용이성**
    - 인터페이스를 통해 구체적인 클래스가 아닌 추상적인 메서드 정의에 의존하기 때문에 구현체를 쉽게 변경할 수 있습니다.
    - 예: `Logger` 인터페이스를 구현한 `FileLogger`, `DatabaseLogger` 등을 상황에 따라 교체 가능.
3. **클래스 간 관계 부여 및 다형성 확장**
    - 상속 관계가 없는 클래스라도 동일한 인터페이스를 구현함으로써 동일한 타입으로 취급할 수 있습니다.
    - 다형성을 통해 코드를 확장성과 유연성이 높은 구조로 설계할 수 있습니다.
    - 예: `Shape` 인터페이스를 구현한 `Circle`, `Rectangle` 클래스는 같은 방식으로 처리 가능.
4. **모듈 간 독립성과 병렬 개발 지원**
    - 인터페이스를 통해 상호 간의 의존성을 낮춰 모듈별 독립적인 개발이 가능하며, 협업에서 개발 기간을 단축시킬 수 있습니다.
    - 인터페이스만 정의되면, 구현체와 호출부를 병렬로 개발 가능.

### 추가 장점
- **의존성 역전 원칙(DIP)을 지원**: 고수준 모듈과 저수준 모듈이 인터페이스를 통해 분리되므로 안정성과 재사용성을 높임.
- **테스트 용이성**: 인터페이스를 통해 Mock 객체를 활용한 단위 테스트 작성이 용이.
```java
// 인터페이스 정의
public interface PaymentProcessor {
    void processPayment(double amount);
}

// 구현체 1: 신용카드 결제
public class CreditCardProcessor implements PaymentProcessor {
    @Override
    public void processPayment(double amount) {
        System.out.println("Processing credit card payment: " + amount);
    }
}

// 구현체 2: 페이팔 결제
public class PayPalProcessor implements PaymentProcessor {
    @Override
    public void processPayment(double amount) {
        System.out.println("Processing PayPal payment: " + amount);
    }
}

// 클라이언트 코드
public class PaymentService {
    private PaymentProcessor processor;

    public PaymentService(PaymentProcessor processor) {
        this.processor = processor;
    }

    public void makePayment(double amount) {
        processor.processPayment(amount);
    }
}

// 사용
public class Main {
    public static void main(String[] args) {
        PaymentProcessor creditCard = new CreditCardProcessor();
        PaymentService service = new PaymentService(creditCard);
        service.makePayment(100.0);

        // 결제 방식 변경
        PaymentProcessor paypal = new PayPalProcessor();
        service = new PaymentService(paypal);
        service.makePayment(200.0);
    }
}

```