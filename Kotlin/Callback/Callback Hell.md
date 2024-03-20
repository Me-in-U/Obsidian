---
tags: kotlin, callback, hell
---
### 콜백 지옥 설명:
#### 정의와 문제점
- 콜백 함수를 너무 많이 중첩해서 사용하면 코드의 가독성과 유지보수가 어려워집니다.
#### 예제 코드
```kotlin
fun taskOne(callback: () -> Unit) {
    // ... 작업
    callback()
}

fun taskTwo(callback: () -> Unit) {
    // ... 작업
    callback()
}

fun main() {
    taskOne {
        taskTwo {
            // ... 더 많은 콜백 중첩
        }
    }
}
```

#### 해결방법
- 코루틴, 비동기 라이브러리, 고차 함수 등을 이용해 콜백 지옥을 해결할 수 있습니다.