---
tags: kotlin, 조건, if, when
---
#### 1. `if`를 표현식으로 사용하기
```kotlin
val max = if (a > b) a else b
```
이렇게 `if`는 값을 반환할 수 있습니다. 즉, 표현식으로 작동합니다.

#### 2. `else if` 체인
```kotlin
if (a > b) {
  println("a is greater")
} else if (a < b) {
  println("b is greater")
} else {
  println("a and b are equal")
}
```
`else if`를 사용해 여러 조건을 체크할 수 있습니다.

#### 3. `when`의 기본 사용법
```kotlin
when (x) {
  1 -> print("x == 1")
  2 -> print("x == 2")
  else -> print("x is neither 1 nor 2")
}
```
`when`은 다양한 조건을 간결하게 표현할 수 있습니다.

#### 4. `when`의 고급 사용법: 패턴 매칭
```kotlin
when (x) {
  is String -> print("String")
  in 1..10 -> print("1 to 10")
  !in 10..20 -> print("Not in 10 to 20")
  else -> print("none of the above")
}
```
`is`나 `in` 키워드와 같은 다양한 패턴 매칭을 사용할 수 있습니다.

#### 5. 최적화 전략
- 작은 범위의 값이 예상되는 경우 `when`을 사용
- 복잡한 조건 로직은 함수로 분리하여 가독성을 높이고, 최적화에 유리하게 함

#### 6. `if`와 `when`의 성능 차이
##### 1. 컴파일된 바이트 코드의 차이점
일반적으로 `when`은 `if`-`else if`-`else` 체인보다 바이트 코드 레벨에서 더 효율적입니다. 그러나 이 <mark style="background: #ADCCFFA6;">차이는 대개 미미</mark>하며, 최적화가 필요한 성능 병목이 아닌 경우 큰 문제가 되지 않습니다.

##### 2. 실제 실행 시간 측정
대규모 데이터에 대해 반복적으로 `if`와 `when`을 실행하여 시간을 측정할 수 있습니다. 하지만 일반적으로 이 둘 사이에는 큰 성능 차이가 없으므로, 이 작업은 종종<mark style="background: #ADCCFFA6;"> 과도한 최적화</mark>로 간주됩니다.

##### 3. 가독성과 유지보수
코드의 가독성과 유지보수성도 성능에 영향을 미칩니다. `when`은 다양한 조건을 깔끔하게 처리할 수 있어, 유지보수가 쉽고 가독성이 높습니다.