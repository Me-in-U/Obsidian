---
tags: java, time
---
```java
//시간 측정 시작
long beforeTime = System.currentTimeMillis(); 
//코드입력

//시간 측정 끝
long afterTime = System.currentTimeMillis();
long exesec = (afterTime-beforeTime);

System.out.println("시간"+ (afterTime-beforeTime)+"ms");
