---
tags:
  - java
  - stream
  - list
---
이제 Stream에서 List로 변환할 때 기존의 긴 Collectors.toList() 를 호출하지 않아도 된다.
```java
private static void old1() {
    Stream<String> stringStream = Stream.of("a", "b", "c");
    List<String> stringList =  stringStream.collect(Collectors.toList());
    for(String s : stringList) {
        System.out.println(s);
    }
}
private static void new1() {
    Stream<String> stringStream = Stream.of("a", "b", "c");
    List<String> stringList =  stringStream.toList();
    for(String s : stringList) {
        System.out.println(s);
    }
}
```
자바 17에서는 toList 이전 동작을 대체하는 메서드가 추가 되었다.
```java
private static void old2() {
    List<Integer> integers = List.of(1,2,3).stream()
    .filter(i -> i > 1)
    .collect(Collectors.toList());
}
private static void new2(){
	List<Integer> integers = List.of(1, 2, 3).stream()
    .filter(i -> i > 1)
    .toList();
}
```
