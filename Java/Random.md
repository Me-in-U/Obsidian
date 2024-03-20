---
tags: java, random
---
``` java
import java.util.Random;
public class RandomExample {
	public static void main(String[] args) {
		//랜덤 객체 생성(디폴트 시드값 : 현재시간) 
		Random random = new Random();
		//시드값 설정을 따로 할수도 있음 
		random.setSeed(System.currentTimeMillis());
		
		System.out.println("n 미만의 랜덤 정수 리턴 : " + random.nextInt(10));
		System.out.println("무작위 boolean 값 : " + random.nextBoolean());
		System.out.println("무작위 long 값 : " + random.nextLong()); 
		System.out.println("무작위 float 값 : " + random.nextFloat());
		System.out.println("무작위 double 값 : " + random.nextDouble()); 
		System.out.println("무작위 정규 분포의 난수 값 :" + random.nextGaussian());
	}
}
```