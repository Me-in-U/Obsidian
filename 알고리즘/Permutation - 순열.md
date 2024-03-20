---
tags: java, math, 순열, 백트랙킹, Permutation
---
```java
import java.util.*;

public class Main {
	static int[] arr;
	static boolean[] check;
	static Stack<Integer> st;
	public static void main(String[] args) {
		System.out.println("========순열========");
		st = new Stack<>();
		arr = new int[] {1,2,3};
		check = new boolean[3];
		permutation(3, 2);
	}
     
	//순열
	static void permutation(int n, int r) {
		if(st.size() == r){
			for(int i : st){
				System.out.print(i+" ");
			}
			System.out.println();
			return;
		}

		for(int i=0; i<n; i++){
			if(!check[i]){
				check[i] = true;
				st.push(arr[i]);
				permutation(n, r);
				st.pop();
				check[i] = false;
			}
		}
	}
}
```