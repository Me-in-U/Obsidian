---
tags:
  - kotlin
  - 지연
  - 초기화
  - lazy
  - 변수
---
`by lazy`는 코틀린에서 지연 초기화 속성을 선언하는 데 사용되는 델리게이트입니다. `by lazy` 델리게이트를 사용하면 속성의 초기화를 처음 접근할 때까지 지연시킬 수 있습니다. 이는 특히 초기화에 많은 리소스가 필요한 경우 유용합니다.

다음은 `by lazy`의 몇 가지 주요 특징 및 사용 방법에 대한 설명입니다:

### 기본 사용법
`by lazy` 델리게이트는 속성 선언에 사용되며, 람다 표현식을 통해 초기화 로직을 제공합니다.
```kotlin
val myLazyValue: String by lazy {     
	println("Initializing")   
	"Hello, World!"
}
```

### 지연 초기화
`by lazy`로 선언된 속성은 처음 접근될 때 초기화됩니다. <mark style="background: #FFB86CA6;">이후에는 이미 초기화된 값을 반환합니다.</mark>
```kotlin
fun main() {
    println("Before accessing myLazyValue")
    println(myLazyValue)  // "Initializing"이 출력된 후 "Hello, World!"가 출력됩니다.
    println(myLazyValue)  // "Hello, World!"만 출력됩니다.
}

```

### 스레드 안전성
`by lazy` 델리게이트는 기본적으로 스레드 안전합니다. 여러 스레드에서 동시에 접근하더라도 속성은 한 번만 초기화됩니다. 이러한 동작은 `LazyThreadSafetyMode` 열거형을 사용하여 변경할 수 있습니다:

- `LazyThreadSafetyMode.SYNCHRONIZED`: (기본값) 여러 스레드에서 안전하게 초기화됩니다.
- `LazyThreadSafetyMode.PUBLICATION`: 여러 스레드에서 동시에 초기화할 수 있으며, 첫 번째 완료된 초기화 값이 사용됩니다.
- `LazyThreadSafetyMode.NONE`: 스레드 안전성을 보장하지 않습니다. 단일 스레드 환경에서만 사용해야 합니다.
```kotlin
val myLazyValue: String by lazy(LazyThreadSafetyMode.NONE) {
    "Hello, World!"
}

```

### `val`과 함께 사용
`by lazy` 델리게이트는 `val` (읽기 전용 속성)과 함께 사용됩니다. <mark style="background: #FF5582A6;">초기화 후에는 속성의 값이 변경되지 않습니다.</mark>

### 사용 사례
`by lazy`는 객체 생성 비용이 높은 속성이나 계산 비용이 높은 속성을 지연 초기화할 때 유용합니다. 이를 통해 애플리케이션의 시작 시간을 줄일 수 있습니다.

이러한 방법으로, `by lazy` 델리게이트는 코틀린에서 효율적인 지연 초기화를 수행하는 강력한 도구로 작용합니다.