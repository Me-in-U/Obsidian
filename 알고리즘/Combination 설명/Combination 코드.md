---
tags: java, math, 재귀, 백트랙킹, 순회, combination, 조합
---
## [백트래킹, 재귀 이용하여 구현](https://bcp0109.tistory.com/15)

```java
//조합 : n 개 중에서 r 개 선택
public class Combination {
    public static void main(String[] args) {
        int n = 4;
        int[] arr = {1, 2, 3, 4};
        boolean[] visited = new boolean[n];

        for (int i = 1; i <= n; i++) {
            System.out.println("\\n" + n + " 개 중에서 " + i + " 개 뽑기");
            comb(arr, visited, 0, n, i);
        }

        for (int i = 1; i <= n; i++) {
            System.out.println("\\n" + n + " 개 중에서 " + i + " 개 뽑기");
            combination(arr, visited, 0, n, i);
        }
    }

    // 백트래킹 사용
    // 사용 예시 : combination(arr, visited, 0, n, r)
    static void combination(int[] arr, boolean[] visited, int start, int n, int r) {
        if (r == 0) {
            print(arr, visited, n);
            return;
        }

        for (int i = start; i < n; i++) {
            visited[i] = true;
            combination(arr, visited, i + 1, n, r - 1);
            visited[i] = false;
        }
    }

    // 재귀 사용
    // 사용 예시 : comb(arr, visited, 0, n, r)
    static void comb(int[] arr, boolean[] visited, int depth, int n, int r) {
        if (r == 0) {
            print(arr, visited, n);
            return;
        }
        
        if (depth == n) {
            return;
        }

        visited[depth] = true;
        comb(arr, visited, depth + 1, n, r - 1);

        visited[depth] = false;
        comb(arr, visited, depth + 1, n, r);
    }

    // 배열 출력
    static void print(int[] arr, boolean[] visited, int n) {
        for (int i = 0; i < n; i++) {
            if (visited[i]) {
                System.out.print(arr[i] + " ");
            }
        }
        System.out.println();
    }
}
```

## 스택
```java
import java.util.*;

​public class Main {

	static int[] arr;
	static boolean[] check;
	static Stack<Integer> st;
	​public static void main(String[] args) {
        
        System.out.println("========조합========");
        st = new Stack<>();
        arr  = new int[] {1,2,3};
        check = new boolean[3];
        combination(0, 2);
 
    }
     
    //조합 
    ​static void combination(int idx, int r) {
        ​if(st.size()== r){
        	​for(int i : st){
                System.out.print(i+" ");
            }
            System.out.println();
            return;
        }
         
        ​for(int i=idx; i<arr.length; i++) {
        	​if(!check[i]) {
        		check[i] = true;
        		st.push(arr[i]);
        		combination(i, r);
        		st.pop();
        		check[i] = false;
        	}
        }
    }
}
```