---
tags: java, lambda
---
``` java
// 람다식 X int c = sum(a, b);
public int sum(int a, int b) { 
	return a + b;`
}
// 람다식 O 
int c = (int a, int b) -> {
	return a + b;
}

// 람다식 X
public int sum(int a, int b) { return a + b; } 
// 람다식 O 
(int a, int b) -> {return a + b;} 

while(variable-- > 0)
variable--; variable > 0; //이 두 가지를 합쳐놓은 것입니다.

int T = 3; int cnt = 10;
while(T-- > 0) {
	System.out.println(cnt--+" 루프 : "+T); 
} 
//10 루프 : 2
//9 루프 : 1 
//8 루프 : 0
```