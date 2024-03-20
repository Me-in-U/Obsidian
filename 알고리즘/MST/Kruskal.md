---
tags: algorithm, graph, kruskal, mst
---
```python
# kruskal Algorithm
def kruskal(graph):
    def find_parent(vertex):
        if parent[vertex] == vertex:
            return vertex
        parent[vertex] = find_parent(parent[vertex])
        return parent[vertex]

    def union(x, y):  # 두 vertex x, y가 속한 두 트리를 하나로 합치는 역할
        root_x, root_y = find_parent(x), find_parent(y)
        # 랭크가 높은 트리 아래에 랭크가 낮은 트리를 병합
        if rank[root_x] < rank[root_y]:
            parent[root_x] = root_y
        elif rank[root_x] > rank[root_y]:
            parent[root_y] = root_x
        else:
            parent[root_y] = root_x
            rank[root_x] += 1

    # 1. 가중치의 오름차순으로 간선들을 정렬: L = 정렬된 간선 리스트
    L = sorted(graph, key=lambda x: x[2])
    print(L)
    # 2. T=Φ // 트리 T를 초기화
    T = []

    # vertices set, 부모 vertex dict(초기값 본인), 랭크 dict 초기화(초기값 0)
    vertices = {vertex for edge in graph for vertex in edge[:2]}
    parent = {vertex: vertex for vertex in vertices}
    rank = {vertex: 0 for vertex in vertices}
    mst_cost = 0
    # 3. while (T의 간선 수 < n-1)
    while len(T) < len(parent) - 1:
        # 4. L에서 가장 작은 가중치를 가진 간선 e를 가져오고, e를 L에서 제거
        # e의 정보(정점 u,v와 가중치 w)
        u, v, w = L.pop(0)
        # 5. if (간선 e가 T에 추가되어 사이클을 만들지 않으면)
        # -> 두 vertex가 같은 vertex에 연결되어있는지 확인
        root_u, root_v = find_parent(u), find_parent(v)
        if root_u != root_v:
            # 6. e를 T에 추가
            T.append((ord(u) - ord('a'), ord(v) - ord('a'), w))
            union(root_u, root_v)
            mst_cost += w

    # 9. Return 트리 T, T는 MST
    return mst_cost, T

kruskal_graph = [
    ('d', 'f', 7),
    ('e', 'f', 9),
    ('b', 'd', 4),
    ('a', 'e', 4),
    ('b', 'f', 2),
    ('a', 'b', 8),
    ('d', 'e', 3),
    ('b', 'c', 1),
    ('c', 'f', 1),
    ('a', 'd', 2)
]
cost1, kruskal_MST = kruskal(kruskal_graph)

print("kruskal mst cost  :", cost1, )
print("kruskal mst graph :", kruskal_MST)
```

