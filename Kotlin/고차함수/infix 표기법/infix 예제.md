---
tags: infix, kotlin, 고차함수
---
```kotlin
infix fun Int.add(a: Int): Int {  
return this + a
} 
val result = 1 add 2  // 3
```

#### 1. `infix`와 DSL
DSL에서 `infix` 표기법을 사용하면, 코드가 더 자연어에 가깝게 보일 수 있습니다.
```kotlin
infix fun String.shouldBe(value: String) {
	if (this != value) {  
		throw AssertionError("Expected $value but was $this")   
	} 
} 
"test" shouldBe "test"
```

#### 2. 연산자 오버로딩
```kotlin
data class Point(val x: Int, val y: Int) {  
	infix operator fun plus(other: Point): Point {
	    return Point(x + other.x, y + other.y)   
	} 
}  
val p1 = Point(1, 1)
val p2 = Point(2, 2)
val p3 = p1 plus p2  // Point(3, 3)
```

#### 3. 고차 함수와 `infix`
고차 함수와 `infix`를 함께 사용하면 더욱 읽기 쉬운 코드를 작성할 수 있습니다.

```kotlin
infix fun <T> T.pipe(f: (T) -> Unit): T {  
	f(this)   
	  return this 
} 
5 pipe { println(it * 2) }
```

#### 4. 컬렉션 연산
```kotlin
infix fun <T> List<T>.has(element: T): Boolean {     return this.contains(element) }  val list = listOf(1, 2, 3) val containsTwo = list has 2  // true
```