---
tags: algorithm, graph, prim, mst
---
```python
# Prim Algorithm
def prim(graph):
    # 1-6. 임의의 정점 p를 선택하고 D[p] = 0으로 설정
    # p에서 나가는 간선을 기반으로 D 초기화
    # p를 제외한 각 정점에 대해 D를 무한으로 초기화(∞)
    vertices = {vertex for edge in graph for vertex in edge[:2]}
    p = list(vertices)[0]  # 임의의 vertex p 선택(0번째)
    D = {vertex: math.inf for vertex in vertices}
    D[p] = 0
    # print(D)  # {'f': 0, 'a': inf, 'c': inf, 'e': inf, 'b': inf, 'd': inf}
    for u, v, w in graph:
        if u == p:
            D[v] = w
        elif v == p:
            D[u] = w
    # print(D)  # {'f': 0, 'a': inf, 'c': 1, 'e': 9, 'b': 2, 'd': 7}

    mst_cost = 0
    # 7. 트리 T를 정점 p로 초기화(임의의 시작점은 바로 추가)
    T = {p}
    # 8. T의 정점 수가 n보다 작은 동안 반복
    while len(T) < len(vertices):
        # 9. T에 없는 정점 중 D[v]가 최소인 정점 vmin 찾음
        vmin = min((D[v], v) for v in vertices if (v not in T))[1]
        mst_cost += D[vmin]
        # 9. T에 있는 정점 u와 vmin을 연결하는 간선을 T에 추가
        T.add(vmin)
        # 10-12. 새로 추가된 정점 vmin을 기반으로 D 업데이트
        for u, v, w in graph:
            if (u == vmin) and (v not in T) and (w < D[v]):
                D[v] = w
            elif (v == vmin) and (u not in T) and (w < D[u]):
                D[u] = w

    # 최소 신장 트리를 구성하는 간선 추출
    mst = [(ord(u) - ord('a'), ord(v) - ord('a'), w)
           for u, v, w in graph if ((u in T) and (v in T)) and ((D[v] == w) or (D[u] == w))]

    # 9. Return mst
    return mst_cost, mst

prim_graph = [
    ('b', 'f', 2),
    ('a', 'd', 2),
    ('a', 'e', 4),
    ('d', 'b', 4),
    ('c', 'f', 1),
    ('d', 'f', 7),
    ('e', 'd', 5),
    ('a', 'b', 3),
    ('e', 'f', 9),
    ('b', 'c', 1)
]

cost2, prim_MST = prim(prim_graph)

print("prim mst cost     :", cost2)
print("prim mst graph    :", prim_MST)
```