---
tags: kotlin, 키워, BufferedReader, BufferedWriter
---
## Kotlin에서 `in` 키워드와 `out` 키워드

코틀린에서 `in`과 `out`은 특별한 의미를 가지는 키워드입니다. 그러나 이들은 다른 문맥에서도 사용될 수 있으며, 그 때의 사용 방법이 다릅니다.

---
### `in` 키워드
1. <mark style="background: #ADCCFFA6;">**범위 연산자</mark>로서의 `in`**: `in` 키워드는 범위 연산자로 사용될 때 키워드로 작동합니다. 예를 들어, `x in 1..10`은 x가 1에서 10 사이에 있는지를 확인합니다.
2. **System.`in`**: 여기서 `in`은 `System` 클래스의 `in` 필드를 참조합니다. 이 경우, `in`은 키워드로 작동하지 않으며, <mark style="background: #D2B3FFA6;">이름 충돌을 피하기 위해 백틱(`` ` ``)으로 감싸줍니다.</mark>

```kotlin
val br = System.`in`.bufferedReader()
```

---
### `out` 키워드
1. <mark style="background: #ADCCFFA6;">**변성 표기</mark>로서의 `out`**: `out` 키워드는 제네릭에서 공변성을 표시할 때 사용됩니다. 예를 들어, `List<out T>`는 T의 하위 타입을 허용하는 List를 의미합니다.
2. **System.out**: 여기서 `out`은 `System` 클래스의 `out` 필드를 참조합니다. 이 경우, `out`은 키워드로 작동하지 않으며, <mark style="background: #D2B3FFA6;">백틱 없이 사용할 수 있습니다.</mark>

kotlinCopy code
```kotlin
val bw = System.out.bufferedWriter()
```

이러한 방식으로, `in`과 `out` 키워드는 코틀린에서 다양한 문맥에서 사용될 수 있으며, 그 의미가 달라집니다.