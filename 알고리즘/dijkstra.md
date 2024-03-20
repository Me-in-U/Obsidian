---
tags: dijkstra, graph
---
```java
public class Main {
	private static ArrayList<Node>[] edges;
	private static int N;
	private static int E;
	private static int INF = Integer.MAX_VALUE;
	
	private static int[] dijkstra(int from) {
	    PriorityQueue<Node> pq = new PriorityQueue<>();
	    int[] distance = new int[N];
	    Arrays.fill(distance, INF);
	    distance[from] = 0;
	    pq.add(new Node(from, 0));
	    while (!pq.isEmpty()) {
	      Node node = pq.poll();
	      int nodeVertex = node.vertex;
	      int nodeWeight = node.weight;
	      if (nodeWeight > distance[nodeVertex])
	        continue;
	      for (Node nextNode : edges[nodeVertex]) {
	        int distance_update = nextNode.weight + distance[nodeVertex];
	        if (distance[nextNode.vertex] > distance_update) {
	          distance[nextNode.vertex] = distance_update;
	          pq.add(new Node(nextNode.vertex, distance_update));
	        }
	      }
	    }
	    return distance;
	}
	private static class Node implements Comparable<Node> {
	    int vertex;
	    int weight;
	
	    public Node(int vertex, int weight) {
		    this.vertex = vertex;
		    this.weight = weight;
	    }
	
	    @Override
	    public int compareTo(Node o) {
			return this.weight - o.weight;
	    }
	}
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	    StringTokenizer st = new StringTokenizer(br.readLine());
	    N = Integer.parseInt(st.nextToken());
	    E = Integer.parseInt(st.nextToken());
	    edges = new ArrayList[N];
	    for (int i = 0; i < N; i++) {
	      edges[i] = new ArrayList<>();
	    }
	    for (int i = 0; i < E; i++) {
	      st = new StringTokenizer(br.readLine());
	      int u = Integer.parseInt(st.nextToken()) - 1;
	      int v = Integer.parseInt(st.nextToken()) - 1;
	      int w = Integer.parseInt(st.nextToken());
	      edges[u].add(new Node(v, w));
	      edges[v].add(new Node(u, w));
	    }
		int[] distance = dijkstra(0);
	}
}
```