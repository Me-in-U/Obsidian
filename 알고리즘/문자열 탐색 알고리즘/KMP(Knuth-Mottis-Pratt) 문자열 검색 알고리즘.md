---
tags: KMP, String, search, algorithm
---
###  Partial Match Table : PMT("aabaabac")
| i   | N[...i]  | 접두사이면서 접미사인 최대 문자열 | pi[i] |     |     |     |     |
| --- | -------- | --------------------------------- | ----- | 
| 0   | a        | (없음)                            | 0     |     |     |     |     |
| 1   | aa       | a                                 | 1     |     |     |     |     |
| 2   | aab      | (없음)                            | 0     |     |     |     |     |
| 3   | aaba     | a                                 | 1     |     |     |     |     |
| 4   | aabaa    | aa                                | 2     |     |     |     |     |
| 5   | aabaab   | aab                               | 3     |     |     |     |     |
| 6   | aabaaba  | aaba                              | 4     |     |     |     |     |
| 7   | aabaabac | (없음)                            | 0     |     |     |     |     |

```java
public static int[] buildPMT(String pattern) {
    int[] pmt = new int[pattern.length()];
    int length = 0;  // length of the previous longest prefix suffix
    // PMT[0] is always 0
    for(int i = 1; i < pattern.length(); i++){
	    while(length != 0 && pattern.charAt(i) != pattern.charAt(length)){
		    length = pmt[length - 1];
	    }
	    if (pattern.charAt(i) == pattern.charAt(length)) {
            pmt[i] = ++length;
        }
    }
    return pmt;
}
```

### PMT 구성 코드 설명
1. PMT 배열 초기화
```java
int[] pmt = new int[pattern.length()];
```
- 패턴 문자열의 길이만큼의 배열을 초기화합니다.
- 이 배열은 각 위치에서의 가장 긴 접두사-접미사의 길이를 저장할 것입니다.

2. 접두사-접미사 길이 변수 초기화
```java
int length = 0;
```
- 가장 긴 접두사-접미사의 길이를 /h저장할 변수입니다.

3. PMT 배열 채우기
```java
for(int i = 1; i < pattern.length(); i++){
   // ...
}
```
- 첫 번째 요소는 항상 0이므로 i는 1부터 시작합니다.

4. 접두사-접미사 길이 재계산
```java
while(length != 0 && pattern.charAt(i) != pattern.charAt(length)){
   length = pmt[length - 1];
}
```
- 현재 i 위치의 문자와 length 위치의 문자가 다르면, length 값을 이전 접두사-접미사의 길이(pmt[length - 1])로 업데이트합니다.

5. 일치하는 경우 PMT 업데이트
```java
if (pattern.charAt(i) == pattern.charAt(length)) {
   pmt[i] = ++length;
}
```
- 문자가 일치하면, length를 증가시킨 다음, pmt[i]에 length 값을 저장합니다.

6. PMT 배열 반환
```java
return pmt;
```
- 완성된 PMT 배열을 반환합니다.

#### KMP
```java
// KMP 문자열 검색 함수
public static void kmpSearch(String text, String pattern) {
    int pLen = pattern.length();
    int[] table = buildPMT(pattern); // 미리 PMT 배열을 생성합니다.
    
    int index = 0;
    for (int i = 0; i <  text.length(); i++) {
        while (index > 0 && text.charAt(i) != pattern.charAt(index)) {
            index = table[index - 1];
        }

        if (text.charAt(i) == pattern.charAt(index)) {
            if (index == pLen - 1) {
                System.out.println("Found pattern at index " + (i - pLen + 1));
                index = table[index];
            } else {
                index++;
            }
        }
    }
}
```

```java
public static void main(String[] args) {
	String text = "ABABDABACDABABCABAB";
	String pattern = "ABABCABAB";
	kmpSearch(text, pattern);
}
```
