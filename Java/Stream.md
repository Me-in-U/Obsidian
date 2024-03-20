---
tags: java, stream, boxed, count, sorted, sort, distinct, max, min, average,
  Map, filter, reduce, match, forEach, collect, partitioning
---
- 스트림은 배열이나 컬렉션(List, Set, Map)으로 원하는 값을 얻을 때 for문 도배를 방지하기 위해 나온 개념

## 선언
```java
Stream<데이터타입> stream명 = Arrays.stream(배열명);
Stream<데이터타입> stream명 = 리스트명.stream(); 
Stream<데이터타입> stream명 = Stream.of('값', '값'....);
```
## 메소드
### boxed()
- Int, Long, Double 배열로 Stream을 만들었을 경우
- 각종 메소드를 사용하기 위해 사용
- 처음에는 붙이지 않고 쓰다가
- 특정 메소드가 안된다 싶으면 붙이는 식으로 사용하면 된다
- 숫자 배열 Stream 사용 시 여러 메소드를 쓰기 위한 boxed 처리
```java
.boxed()
System.out.println(Arrays.stream(arr).boxed());
```
### count() 배열, 컬렉션 크기 확인
``` java
.count()
배열, 컬렉션 크기 확인

System.out.println(Arrays.stream(arr).count());
System.out.println(list.stream().count());
```
### sorted() 정렬/역정렬
``` java
.sorted()
System.out.println(Arrays.stream(arr).boxed().sorted().collect(Collectors.toList()));
System.out.println(list.stream().sorted().collect(Collectors.toList()));

.sorted(Comparator.reverseOrder())
System.out.println(Arrays.stream(arr).boxed().sorted(Comparator.reverseOrder()).collect(Collectors.toList()));
System.out.println(list.stream().sorted(Comparator.reverseOrder()).collect(Collectors.toList()));
```
### 값 가져오기
``` java
.findFirst()
//스트림의 처음 값 가져오기
System.out.println(Arrays.stream(arr).findFirst().getAsInt());
System.out.println(list.stream().findFirst().get());

.skip(배열크기 - 1).findFirst()
//스트림의 마지막 값 가져오기
System.out.println(Arrays.stream(arr).skip(arr.length - 1).findFirst().getAsInt());
System.out.println(list.stream().skip(list.size() - 1).findFirst().get());

.skip(값)
//값의 인덱스까지 생략하고 나머지를 가져옴
// skip(값) N개 생략하고
System.out.println(Arrays.stream(arr).boxed().skip(1).collect(Collectors.toList()));
System.out.println(list.stream().skip(1).collect(Collectors.toList()));

.limit(값)
//값의 인덱스까지 가져옴
// limit(값) N개 까지
System.out.println(Arrays.stream(arr).boxed().limit(2).collect(Collectors.toList()));
System.out.println(list.stream().limit(2).collect(Collectors.toList()));
```
### distinct() 중복 생략
``` java
.distinct()
// distinct() 중복 생략
System.out.println(Arrays.stream(arr).boxed().distinct().collect(Collectors.toList()));
System.out.println(list.stream().distinct().collect(Collectors.toList()));
```
### 최대값 / 최소값 / 평균 / 합
``` java
.max(데이터타입::compare)
System.out.println(Arrays.stream(arr).boxed().max(Integer::compare).get());
System.out.println(list.stream().max(Integer::compare).get());

.min(데이터타입::compare)
System.out.println(Arrays.stream(arr).boxed().min(Integer::compare).get());
System.out.println(list.stream().min(Integer::compare).get());

.average()
// 배열일 경우에는 바로 사용 가능하지만
//list, set, map의 경우에는 mapToDouble()을 이용해
//한번 바꿔준 후 사용해야 함 하단 예제 코드 참고
System.out.println(Arrays.stream(arr).average().getAsDouble());
System.out.println(list.stream().mapToDouble(Integer::doubleValue).average().getAsDouble());

.sum()
System.out.println(Arrays.stream(arr).sum());
System.out.println(list.stream().mapToInt(Integer::intValue).sum());
```
### map((파라미터) -> 코드)
- 람다(Lambda)를 이용한 가공
- 각 인덱스의 값을 파라미터로 넘기고 코드를 수행한다
- 주로 값을 바꿔주거나 더해주거나 할 때 사용하게 된다
- map은 코드 부분에서 ***메소드 사용이 불가능***한데 이건 아래의 forEach를 사용해주면 된다
``` java
.map((파라미터) -> 코드)

// map(값을 원하는대로 가공)
System.out.println("map 1이면 true 아니면 false 예제");
System.out.println(Arrays.stream(arr).boxed().map(val -> val == 1).collect(Collectors.toList()));
System.out.println(list.stream().map(val -> val == 1).collect(Collectors.toList()));

// map 값마다 10 더하기 예제
System.out.println("map 값마다 10 더하기 예제");
System.out.println(Arrays.stream(arr).boxed().map(val -> val = val + 10).collect(Collectors.toList()));
System.out.println(list.stream().map(val -> val = val + 10).collect(Collectors.toList()));	
		
// map 값 반올림 예제
System.out.println("map 값 반올림 예제");
System.out.println(Arrays.stream(arr).boxed().map(val -> Math.round(val*10)/10.0).collect(Collectors.toList()));
System.out.println(list.stream().map(val -> Math.round(val*10)/10.0).collect(Collectors.toList()));
```
### forEach((파라미터) -> {코드})
- 각 인덱스의 값을 파라미터로 넘기고 코드를 수행
	- (값마다 다른 ***메소드를 수행***한다거나 할때 사용) 
``` java
.forEach((파라미터) -> {코드})

// forEach(모든 값마다 입력한 내용 수행)
System.out.println("forEach(모든 값마다 입력한 내용 수행)");
Arrays.stream(arr).boxed().forEach(val -> System.out.println("ForEach 출력! : " + val));
list.stream().forEach(val -> System.out.println("ForEach 출력! : " + val));

map과 forEach는 흡사하지만
map은 값만 바꿔주는 정도고
forEach는 if else나 메소드 등을 사용한느 것이 중점이 되겠다
```
### Match((파라미터) -> {코드})
- anyMatch는 스트림 중 하나의 값이라도 조건에 맞으면 true
- noneMatch는 스트림 중 하나의 값도 조건에 맞지 않으면 true
- allMatch는 스트림의 값이 모두 조건에 맞아야 true
``` java
.anyMatch((파라미터) -> {코드})
.noneMatch((파라미터) -> {코드})
.allMatch((파라미터) -> {코드})

List<String> names = Arrays.asList("Eric","Elena","Java");
// anyMatch(스트림에서 조건이 하나라도 맞으면) 
System.out.println("anyMatch(스트림에서 조건이 하나라도 맞으면) TRUE");
System.out.println(Arrays.stream(arr).anyMatch(val -> val == 1));
System.out.println(list.stream().anyMatch(val -> val == 1));
boolean anyMatch = names.stream().anyMatch(name -> name.contains("a"));
		
// noneMatch(스트림에서 조건이 하나도 안맞으면)
System.out.println("noneMatch(스트림에서 조건이 하나도 안맞으면) TRUE");
System.out.println(Arrays.stream(arr).noneMatch(val -> val == 99));
System.out.println(list.stream().noneMatch(val -> val == 99));
boolean noneMatch = names.stram().noneMatch(name -> name.endsWith("s"));
		
// allMatch(스트림의 값이 모두 조건과 맞아야)
System.out.println("allMatch(스트림의 값이 모두 조건과 맞아야) TRUE");
System.out.println(Arrays.stream(arr).allMatch(val -> val == 1));
System.out.println(list.stream().allMatch(val -> val == 1));
boolean allMatch = names.stream().allMatch(name -> name.length() > 3);
```
### filter(파라미터) -> {코드})
- 코드에 맞는 값만 가져온다
```java
.filter(파라미터) -> {코드})

// filter (특정 값만 허용)
System.out.println("filter (특정 값만 허용)");
System.out.println(Arrays.stream(arr).boxed().filter(val -> val == 10).collect(Collectors.toList()));
System.out.println(list.stream().filter(val -> val == 10).collect(Collectors.toList()));
```
### reduce(값, 데이터타입::sum)
- 스트림의 값을 모두 하나로 합칠때 사용하는데
- 데이터타입과 sum으로 하나로 합친 뒤
- 마지막에 값을 더해서 가져오게 된다 (String의 경우에는 값, String::concat을 사용)
``` java
.reduce(값, 데이터타입::sum)
// reduce (스트림 값을 모두 하나로 합치기)
System.out.println("reduce (스트림 값을 모두 하나로 합치기) 다 합치고 5 더하기 예제");
System.out.println(Arrays.stream(arr).reduce(5, Integer::sum));
System.out.println(list.stream().reduce(5, Integer::sum));
```
### toArray() toList()
``` java
.toArray();
배열, 컬렉션(List, Set, Map) 형태로 가져오는 경우라면 배열의 경우에는 끝에 붙임
```
### collect
- 자바의 `collect` 메서드는 스트림의 요소들을 수집하여 다양한 형태의 결과를 생성하는 데 사용됩니다
``` java
.collect(Collectors.toList());
에서 List만 Set, Map으로 바꿔주면 된다

.collect(Collectors.counting());
해당하는 갯수 반환
```
####  **문자열로 수집**
``` java
String joined = stream.collect(Collectors.joining(", "));
.collect(Collectors.joining("|"));
//모든 값을 합치면서 |를 붙여줌
//"" 붙이면 그냥 값만 다 붙이게 됨

.collect(Collectors.averagingInt(val -> Integer.parseInt(val))
.collect(Collectors.averagingDouble(val -> Double.parseDouble(val))
.collect(Collectors.averagingLong(val -> Long.parseLong(val))
값을 int, double, long 형태로 변환한 뒤
double 형태의 평균을 구해 반환
```
List, Set Map으로 수집
``` java
List<String> list = stream.collect(Collectors.toList());

Set<String> set = stream.collect(Collectors.toSet());

Map<String, Integer> map = stream.collect(Collectors.toMap(Function.identity(), String::length));
```
#### **그룹화**
```java
.collect(Collectors.groupingBy(Function.identity(), Collectors.counting())
//이름, 갯수의 형태로 Map<String, Long>로 반환을 해 준다
//1,1,1,2,2 이렇게 들었으면 "1" , 3 이런식으로 들어간다는 얘기
//오라클에서 그룹핑 해서 가져오는 것과 동일한 개념이라고 보면 된다
		 
Map<Integer, List<String>> groups = stream.collect(Collectors.groupingBy(String::length));
```
#### **파티셔닝**
``` java
.collect(Collectors.partitioningBy((파라미터) -> {코드})
//조건에 맞으면 true, 아니면 false로 list를 만들고
//Map<Boolean, List<String>> 형태로 반환한다

Map<Boolean, List<String>> partition = stream.collect(Collectors.partitioningBy(s -> s.length() > 3));

```
### **통계 정보 수집**
- 스트림의 요소들에 대한 통계 정보(예: 합계, 평균, 최대, 최소 등)를 수집할 수 있습니다.
```java
IntSummaryStatistics stats = stream.collect(Collectors.summarizingInt(Integer::intValue));
```

### **Iterating**
```java
names.stream().forEach(Systemp.out::println);
```