---
tags: kotlin, typealias
---
#### 기본적인 `typealias` 사용법
```kotlin
typealias Username = String 
typealias Password = String  
fun login(user: Username, pass: Password) {   // 로그인 로직 }
```
---
#### 함수 타입에 대한 `typealias`
```kotlin
typealias ClickHandler = (Button, Event) -> Unit  fun setClickListener(clickHandler: ClickHandler) {   // 클릭 이벤트 설정 }
```
---
#### 제네릭을 사용하는 `typealias`
```kotlin
typealias StringList = List<String>
typealias IntMap<V> = Map<Int, V>
```
---
#### 중첩된 타입에 대한 `typealias`
```kotlin
typealias UserMap = Map<Username, List<Password>>
```

#### 람다 표현식과 고차 함수
```kotlin
typealias SimpleCallback = () -> Unit 
typealias Mapper<T, R> = (T) -> R
```

#### 조건부 `typealias`
```kotlin
expect typealias PlatformString: String
```

#### 플랫폼 타입
```kotlin
typealias JString = java.lang.String
```

#### 타입 전환
```kotlin
typealias Point2D = Pair<Int, Int>
```

#### 인터페이스와의 활용
```kotlin
typealias Clickable = (View) -> Unit 
interface ClickableElement {   
	val onClick: Clickable
}
```
