---
tags: algorithm, java, bfs, Deque, graph
---
0-1 BFS 알고리즘은 일반적인 BFS(Breadth-First Search) 알고리즘의 변형으로, 가중치가 0 또는 1인 그래프에서 최단 경로를 찾을 때 사용됩니다. 
일반 BFS와 차이점은 큐 대신 덱을 사용해 가중치에 따라 노드를 삽입하는 것입니다.

요약: 0-1 BFS 알고리즘은 가중치가 0 또는 1인 그래프에서 최단 경로를 찾는 알고리즘입니다.

#### 단계별 행동 계획
1. 그래프의 정보와 출발점을 입력 받음
2. 덱 자료구조를 선언함.
3. 출발점을 덱에 삽입하고, 거리를 0으로 설정.
4. 덱이 비어있지 않은 동안 다음을 반복:
	- 덱의 앞에서 노드를 꺼냄.
	- 해당 노드와 연결된 모든 인접 노드를 검사.
	- 가중치가 0인 경우, 덱의 앞에 삽입.
	- 가중치가 1인 경우, 덱의 뒤에 삽입.
5. 목적지 노드까지의 최단 거리를 출력 또는 반환.

```java
package BAEKJOON.Gold.Gold_IV.P13549번_숨바꼭질_3; 
  
 import java.io.BufferedReader; 
 import java.io.IOException; 
 import java.io.InputStreamReader; 
 import java.util.ArrayDeque; 
 import java.util.Arrays; 
 import java.util.Deque; 
 import java.util.StringTokenizer; 
  
 public class Main { 
   public static void main(String[] args) throws IOException { 
     BufferedReader br = new BufferedReader(new InputStreamReader(System.in)); 
     StringTokenizer st = new StringTokenizer(br.readLine()); 
     int N = Integer.parseInt(st.nextToken()); 
     int K = Integer.parseInt(st.nextToken()); 
     int[] time = new int[2000001]; 
     Arrays.fill(time, Integer.MAX_VALUE); 
     time[N] = 0; 
     Deque<Integer> dq = new ArrayDeque<>(); 
     dq.add(N); 
     while (!dq.isEmpty()) { 
       int now = dq.poll(); 
       if (now == K) { 
         System.out.println(time[K]); 
         break; 
       } 
       int tp = now * 2; 
       if (tp <= 200000 && time[tp] > time[now]) { 
         time[tp] = time[now]; 
         dq.addFirst(tp); 
       } 
       int walkLeft = now - 1; 
       if (0 <= walkLeft && time[walkLeft] > time[now]) { 
         time[walkLeft] = time[now] + 1; 
         dq.addLast(walkLeft); 
       } 
       int walkRight = now + 1; 
       if (walkRight <= 200000 && time[walkRight] > time[now]) { 
         time[walkRight] = time[now] + 1; 
         dq.addLast(walkRight); 
       } 
     } 
   } 
 }
```