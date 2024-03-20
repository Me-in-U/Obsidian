---
tags: java, arrays, 깊은복사, fill, copy
---
```java
1차원 배열의 비교와 출력
equals(), toString()
System.out.println("nums detail: "+Arrays.toString(nums));

다차원 배열의 비교와 출력
deepEquals(), deepToString()

복사
Arrays.copyOf(배열이름,배열길이);
int target[] = Arrays.copyOf(nums, nums.length);
copyOf(), copyOfRange()

채우기
fill(), setAll()

배열을 List로 변환
asList(Object... a)
    ex) List list = Arrays.asList(new Integer[]{1,2,3,4,5})```

