---
tags: java, StringBuilder, StringBuffer
---
```java
/*StringBuffer는 각 메소드 별로 synchronized keyword가 존재하여
멀티 스레드 상태에서 동기화를 지원하고 StringBuilder는 단일 스레드 환경에서만
사용하도록 설계되어 있습니다.

StringBuilder가 StringBuffer보다 속도는 더 빠르지만
현업에서는 언제 멀티스레드 환경에서 돌아가지 알지 못하기에
안정적인 StringBuffer로 통일하여 코딩하는것이 좋습니다.
*/

String s = "abcdefg";
StringBuffer sb = new StringBuffer(s);
StringBuilder sb = new StringBuilder();

sb.append(nums[i]).append('\n');
sb[age].append(age).append(" ").append(name).append("\n");
System.out.println(sb);

sb //처음상태
sb.toString()  //String 변환하기
sb.substring(2,4) //문자열 추출하기
sb.insert(2,"추가") //문자열 추가하기
sb.delete(2,4)   //문자열 삭제하기
sb.append("hijk")  //문자열 붙이기
sb.length()  //문자열의 길이구하기
sb.capacity()  //용량의 크기 구하기
sb.reverse()  //문자열 뒤집기
java```

![[Untitled.png]]