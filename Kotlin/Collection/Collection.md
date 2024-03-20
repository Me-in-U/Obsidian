---
tags:
  - kotlin
  - list
  - Map
  - Set
  - collecion
  - 불변
  - 가변
  - immutable
  - mutable
---
### 1. 불변 컬렉션 (Immutable Collections)
불변 컬렉션은 한 번 생성되면 그 구조를 변경할 수 없습니다. 즉, 요소를 추가하거나 제거할 수 없습니다. 불변 컬렉션은 안전하고 예측 가능한 작업을 보장합니다.

- **List**: 순서가 있는 컬렉션입니다. `listOf` 함수를 사용하여 생성할 수 있습니다.
- **Set**: 중복 없는 요소의 집합을 나타내며, 순서가 없습니다. `setOf` 함수를 사용하여 생성할 수 있습니다.
- **Map**: 키-값 쌍의 집합을 나타냅니다. `mapOf` 함수를 사용하여 생성할 수 있습니다.

---

### 2. 가변 컬렉션 (Mutable Collections)
가변 컬렉션은 구조를 변경할 수 있는 컬렉션입니다. 즉, 요소를 추가하거나 제거할 수 있습니다.

- **MutableList**: 순서가 있는 컬렉션으로, 요소를 추가하거나 제거할 수 있습니다. `mutableListOf` 함수를 사용하여 생성할 수 있습니다.
- **MutableSet**: 중복 없는 요소의 집합을 나타내며, 요소를 추가하거나 제거할 수 있습니다. `mutableSetOf` 함수를 사용하여 생성할 수 있습니다.
- **MutableMap**: 키-값 쌍의 집합을 나타내며, 요소를 추가하거나 제거할 수 있습니다. `mutableMapOf` 함수를 사용하여 생성할 수 있습니다.

---

### 예제
```kotlin
// 불변 리스트
val immutableList = listOf(1, 2, 3)

// 가변 리스트
val mutableList = mutableListOf(1, 2, 3)
mutableList.add(4) // 요소 추가

// 불변 세트
val immutableSet = setOf(1, 2, 3)

// 가변 세트
val mutableSet = mutableSetOf(1, 2, 3)
mutableSet.add(4) // 요소 추가

// 불변 맵
val immutableMap = mapOf("key1" to 1, "key2" to 2)

// 가변 맵
val mutableMap = mutableMapOf("key1" to 1, "key2" to 2)
mutableMap["key3"] = 3 // 요소 추가

```