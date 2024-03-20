---
tags: kotlin, callback
---
### 콜백 함수 설명:
#### 기본 개념
- 콜백 함수는 특정 이벤트가 발생하거나 특정 조건이 충족되면 자동으로 호출되는 함수입니다.

#### 일반적 사용 예
- 파일 읽기, 네트워크 요청, 이벤트 리스너 등에서 자주 사용됩니다.

#### 기초 예제:
```kotlin
// 1. main 함수
fun main() {
    // 4. 이벤트 리스너 함수 호출
    eventListener(::callback)
}

// 2. 콜백 함수 정의
fun callback(message: String) {
    println("콜백 함수 호출됨: $message")
}

// 3. 이벤트 리스너 함수 작성
fun eventListener(callback: (String) -> Unit) {
    println("이벤트 리스너 작동")
    // 여기에서는 단순히 예시로 콜백 함수를 호출하겠습니다.
    callback("이벤트 발생!")
}
```

```kotlin
fun doSomethingAsync(callback: (result: String) -> Unit) {
    // 비동기 작업
    val result = "작업 완료"
    callback(result)
}

fun main() {
    doSomethingAsync { result ->
        println("콜백 함수에서의 출력: $result")
    }
}
```

### 이벤트 리스너에서의 콜백 함수 설명:
#### 기본 개념
- 이벤트 리스너는 사용자의 클릭, 키 입력 등 특정 이벤트가 발생했을 때 실행되는 코드 블럭을 말합니다.

#### 콜백 함수 적용
- 이벤트 리스너 내에서 콜백 함수를 정의하거나 사용하여 이벤트 발생 시 특정 작업을 수행할 수 있습니다.

#### 코틀린 코드 예시
```kotlin
// Android 환경에서의 예시
button.setOnClickListener {
    // 콜백 함수
    println("버튼이 클릭되었습니다.")
}
```
