---
tags: java, lambda
---
##  람다 표현식이란?
- **익명 함수(anonymous function)**로, 이름 없이 정의되는 메서드의 구현체
- 자바 8부터 도입되어 기존의 익명 내부 클래스(anonymous inner class)를 대체
- 단 한 개의 추상 메서드만 가진 **함수형 인터페이스(functional interface)**에 대한 간결한 구현 수단을 제공

## 람다 표현식의 구현 조건 및 사용법
- **단 하나의 추상 메서드:** 람다 표현식은 단 하나의 추상 메서드를 가진 인터페이스(예: `Runnable`, `Comparator<T>`, `Predicate<T>`)에 대한 구현체로 사용됩니다.
- **@FunctionalInterface 어노테이션:** 개발자가 의도한 함수형 인터페이스임을 명시하기 위해, 인터페이스 선언 시 `@FunctionalInterface` 어노테이션을 사용할 수 있습니다.

### 문법
```java
(매개변수 목록) -> { 
    // 실행할 코드 블록 
}
```
- **매개변수 목록:** 매개변수의 타입은 생략할 수 있으며, 컴파일러가 문맥(타입 추론)을 통해 자동으로 결정합니다.
- **화살표(->):** 매개변수와 실행 코드를 구분하는 역할을 합니다.
- **코드 블록:** 중괄호 `{}`를 사용하여 여러 문장을 포함할 수 있으며, 단일 문장일 경우 중괄호와 `return` 문을 생략할 수 있습니다.

##### 예제 1: Runnable 인터페이스 구현
```java
Runnable runnable = () -> System.out.println("람다 표현식 실행!");
new Thread(runnable).start();
```
##### 예제 2: Comparator 인터페이스 구현
```java
Comparator<Integer> comparator = (a, b) -> Integer.compare(a, b);
int result = comparator.compare(5, 3); // result는 양수
```

### 캡처와 변수 사용
- **effectively final 변수:** 람다 표현식 내부에서 외부 변수를 사용할 경우, 해당 변수는 변경되지 않아야 합니다. 즉, 변수는 **effectively final** 상태여야 합니다.
- **안전한 캡처:** 외부 변수의 값을 안전하게 캡처하여 사용할 수 있으므로, 병행 처리 시에도 안전한 코드를 작성할 수 있습니다.

``` java
// 람다식 X int c = sum(a, b);
public int sum(int a, int b) { 
	return a + b;`
}
// 람다식 O 
int c = (int a, int b) -> {
	return a + b;
}

// 람다식 X
public int sum(int a, int b) { return a + b; } 
// 람다식 O 
(int a, int b) -> {return a + b;} 

while(variable-- > 0)
variable--; variable > 0; //이 두 가지를 합쳐놓은 것입니다.

int T = 3; int cnt = 10;
while(T-- > 0) {
	System.out.println(cnt--+" 루프 : "+T); 
} 
//10 루프 : 2
//9 루프 : 1 
//8 루프 : 0
```
