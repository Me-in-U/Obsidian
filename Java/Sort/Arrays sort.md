---
tags: java, sort, 내림차순, 오름차순, arrays
---
```java
Arrays.sort("배열이름"); 낮은수부터 정렬
Arrays.sort(scores); 
Arrays.sort(arr, 0, 4); // 0,1,2,3 요소만 정렬

Collections.sort(arr);
```

## 내림차순 정렬하기

```java
//포장클래스 Integer 사용하여서 scores배열 생성
Integer scores[] = {80, 50, 30, 90, 75, 85, 77 };

// Collections.reverseOrder() 내림차순 정렬 인수 추가
Arrays.sort(scores, Collections.reverseOrder());

// 부가적인 기능 Collections.reverseOrder() 사용하기 위해서
// 기본 int타입 데이터를 포장클래스 integer를 이용해서 객체화
```