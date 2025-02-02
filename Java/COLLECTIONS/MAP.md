---
tags: java, collections, Map, HashMap, LinkedHashMap, TreeMap, KeySet, entrySet,
  key, value, Iterator
---
## 특징
- 키(key)와 값(value)의 쌍으로 데이터를 다루는 경우 Map을 사용
- HashMap은 해시 함수를 통해 '키'와 '값'이 저장되는 위치를 결정하므로, 사용자는 그 위치를 알 수 없고, 삽입되는 순서와 들어 있는 위치 또한 관계가 없습니다.
- 많은 양의 데이터를 검색하는 데 있어서 뛰어난 성능
- 값은 중복 저장될 수 있지만 키는 중복 저장될 수 없습니다

treemap : key는 이진탐색트리, key는 null 불가능
hashmap : key null값 1번 허용

## 코드 예제
``` java
import java.util.HashMap; 
import java.util.LinkedHashMap; 
import java.util.TreeMap; 
import java.util.Map;
```
### 선언
``` java
Map<형, 형> map = new HashMap<>();
HashMap<Integer,String> map = new HashMap<>(); 
TreeMap<Integer,String> map = new TreeMap<>();
```
<값 추가/제거>
``` java
//키 값이 Map 내부에 존재한다면 기존의 값은 새로 입력되는 값으로 대치됩니다.
Map.put(1,"사과"); //값 추가

//기본값 아니면 +1 
for (int i = 0; i < N; i++) { 
	Long num = Long.parseLong(br.readLine());
	map.put(num, map.getOrDefault(num, 0) + 1); 
} 

//key값 1 제거 오직 키값으로만 Map의 요소를 삭제
Map.remove(1);
//모든 값 제거
map.clear();
```

### <값 출력>
#### Map출력
``` java
//전체 출력 : {1=사과, 2=바나나, 3=포도} 
System.out.println(map);
//key값 1의 value얻기 : 사과
System.out.println(map.get(1));
```
#### TreeMap 출력
``` java
//전체 출력 : {1=사과, 2=복숭아, 3=수박}
System.out.println(map); 
//key값 1의 value얻기 : 사과 
System.out.println(map.get(1));
//최소 Entry 출력 : 1=사과 
System.out.println(map.firstEntry());
//최소 Key 출력 : 1 
System.out.println(map.firstKey());
//최대 Entry 출력: 3=수박 
System.out.println(map.lastEntry());
//최대 Key 출력 : 3
System.out.println(map.lastKey());
```
#### Map 전체 값 출력
entrySet
``` java
//entrySet() 활용 - key와 value 모두가 필요할 경우
for (Entry<Integer, String> entry : map.entrySet()) {
	System.out.println("[Key]:" + entry.getKey() + " [Value]:" + entry.getValue());
}

//entrySet().iterator()
Iterator<Entry<Integer, String>> entries = map.entrySet().iterator(); 
while(entries.hasNext()){
	Map.Entry<Integer, String> entry = entries.next();
	System.out.println("[Key]:" + entry.getKey() + " [Value]:" + entry.getValue());
}
```
##### KeySet
``` java
//KeySet() 활용 - key 값만 필요할 경우
for(Integer i : map.keySet()){
	//저장된 key값 확인
	System.out.println("[Key]:" + i + " [Value]:" + map.get(i));
}

//keySet().iterator()
Iterator<Integer> keys = map.keySet().iterator();
while(keys.hasNext()){
	int key = keys.next();
	System.out.println("[Key]:" + key + " [Value]:" + map.get(key));
}
```

## <검색>
### key값으로 value값 찾기 / 바꾸기
``` java
for(int i = 0; i < N; i++){
	int key = Integer.parseInt(st.nextToken());
	if(map.containsKey(key))
		map.put(key, (map.get(key) + 1));
	else
		map.put(key, 1);
}
```

### value값으로 key값 찾기
``` java
for (Map.Entry<String, Integer> entry : map.entrySet()) {
	String key = entry.getKey();
	Integer value = entry.getValue();
	System.out.println("Iterating, key: " + key + ", value: " + value);
	if (value == 2) {
		System.out.println("key of the value 2: " + key);
	}
}
```
### value 값만 모두 가져오기
``` java
for (int val : map.values()) {
	result *= (val + 1);
}
```

## [<정렬>](https://codechacha.com/ko/java-sort-map/)
### key로 정렬
``` java
List<String> keyList = new ArrayList<>(map.keySet());
keyList.sort((s1, s2) -> s1.compareTo(s2));
//keyList.sort(String::compareTo);
for (String key : keyList) {
	System.out.println("key: " + key + ", value: " + map.get(key));
}
```
### Value로 정렬(Sort by value)
``` java
List<String> valueList = new ArrayList<>(map.values()); valueList.sort(String::compareTo);
for (String value : valueList) {
	System.out.println("Value: " + value);
}
```


## Map 클래스 주요 메서드
``` java
V put(K Key, V value);
boolean containsKey(Object Key);
boolean containsValue(Object value);
Set<Map.Entry<K,V>> entrySet();
Set<K> keySet() V get(Object key);
boolean isEmpty();
int Size() Collection<V> values();
void clear() V remove(Object Key)
```

### 찾는 키가 존재한다면 찾는 키의 값을 반환하고 없다면 기본 값을 반환하는 메서드
``` java
//getOrDefault(Object key, V DefaultValue)
import java.util.HashMap;
public class MapGetOrDefaultEx { 
	public static void main(String arg[]) {
		String [] alphabet = { "A", "B", "C" ,"A"};
		HashMap<String, Integer> hm = new HashMap<>();
		for(String key : alphabet)
			hm.put(key, hm.getOrDefault(key, 0) + 1);
		System.out.println("결과 : " + hm); // 결과 : {A=2, B=1, C=1}
	}
}
```