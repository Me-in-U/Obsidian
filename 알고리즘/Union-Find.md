Union-Find 알고리즘은 트리 구조를 사용하여 disjoint set들을 관리합니다. 이 알고리즘은 두 주요 연산, Union과 Find,을 제공합니다. Union 연산은 두 집합을 하나로 합치고, Find 연산은 주어진 원소가 어떤 집합에 속하는지 찾아냅니다. 아래는 Union-Find 알고리즘의 기본적인 구현입니다:

```java
public class UnionFind {
    private int[] parent;
    private int[] rank;

    public UnionFind(int size) {
        parent = new int[size];
        rank = new int[size];
        for (int i = 0; i < size; i++) {
            parent[i] = i;
            rank[i] = 0;
        }
    }

    public int find(int x) {
        if (parent[x] != x) {
            parent[x] = find(parent[x]);
        }
        return parent[x];
    }

    public void union(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);
        if (rootX != rootY) {
            if (rank[rootX] > rank[rootY]) {
                parent[rootY] = rootX;
            } else {
                parent[rootX] = rootY;
                if (rank[rootX] == rank[rootY]) {
                    rank[rootY]++;
                }
            }
        }
    }
}

```

```java
package BAEKJOON.Gold.Gold_V.P1717번_집합의_표현;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
  protected static int[] parent;

  public static void main(String[] args) throws NullPointerException, IOException {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    StringTokenizer st = new StringTokenizer(br.readLine());
    StringBuilder sb = new StringBuilder();
    int n = Integer.parseInt(st.nextToken());
    int m = Integer.parseInt(st.nextToken());
    parent = new int[n + 1];
    for (int i = 1; i <= n; i++)
      parent[i] = i;
    for (int i = 0; i < m; i++) {
      st = new StringTokenizer(br.readLine());
      int calculate = Integer.parseInt(st.nextToken());
      int a = Integer.parseInt(st.nextToken());
      int b = Integer.parseInt(st.nextToken());
      if (calculate == 0)
        union(a, b);
      else
        sb.append(findParent(a) == findParent(b) ? "YES" : "NO").append('\n');
    }
    System.out.print(sb.toString());
  }

  public static int findParent(int x) {
    if (x == parent[x])
      return x;
    parent[x] = findParent(parent[x]);
    return parent[x];
  }

  public static void union(int a, int b) {
    a = findParent(a);
    b = findParent(b);
    if (a != b) {
      if (a < b)
        parent[b] = a;
      else
        parent[a] = b;
    }
  }
}
```