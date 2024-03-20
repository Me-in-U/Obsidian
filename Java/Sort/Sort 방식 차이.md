---
tags: java, sort, TimeComplexity
---
![[Sort Methods.png]]
Arrays.sort(DualPivotQuickSort)
Collections.sort(TimSort)

	Tim Sort         O(N)          O(N logN)    O(N logN)
배열을 2^x 단위 만큼 쪼갠다음에 각각에 대해서 삽입 정렬을 실시한다.

이후 Merge Sort 를 통해서 값을 합쳐준다.

작은 덩어리일 때는 삽입 정렬이 Quick Sort 보다 빠르기 때문에 작은 n 단위로 쪼개고 그 후 병합을 해주는 것이 기본적인 아이디어이다.

동작 시간은 O(nlog(n))의 형태가 되고 그 과정중에서 값을 최대한 효율적으로 만들기 위해 여러 최적화 기법이 사용되고 있다.
![[Sort Type.png]]