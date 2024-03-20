---
tags: java, math, ccw
---
[https://degurii.tistory.com/47](https://degurii.tistory.com/47)
[https://rebro.kr/10](https://rebro.kr/10)
[https://snowfleur.tistory.com/98](https://snowfleur.tistory.com/98)


CCW 알고리즘은 시계반대방향일 때양수, 시계방향일 때음수,  평행일 때0을 반환한다.

각각의 점을 A(x1, y1) , B(x2, y2), C(x3, y3) 이라고 좌표를 두고, A,B,C 순서로 방향관계를 구한다면,

### CCW 함수의 return값은
>(x2 - x1)(y3 - y1) - (x3 - x1)(y2 - y1) 
>= (x1y2 + x2y3 + x3y1) - (x2y1 + x3y2 + x1y3) 이 된다.

![[ccw1.png]]
![[ccw2.png]]

### 외적은 다음과 같은 특징이 있다.
- 기호로는 X를 사용한다
- 두 벡터를 외적 하면 두 벡터의 수직 벡터 즉 벡터가 나온다 내적은 스칼라 값이 나온다.
- 외적은 교환 법칙이 성립하지 않는다. a x b와 b x a는 다르다.
- 두 벡터의 외적은 두 벡터가 만들어내는 평행사변형의 넓이이다.

![[Matrix notation.png]]

### 오른손 법칙을 통한 방향 알아내기
![[오른손 법칙.png]]
오른손으로 해당하는 방향으로 쥐었을 때의 엄지 방향이 그 수직 벡터의 방향이 된다. 이 그림에서는 u x v이기 때문에

u벡터에서 v 벡터로 손을 감았을 때 엄지가 위에 있기 때문에 두 벡터의 수직 벡터는 위를 바라보게 된다. 만약에 v x u 였다면 반대로 엄지가 아래를 향하게 된다.