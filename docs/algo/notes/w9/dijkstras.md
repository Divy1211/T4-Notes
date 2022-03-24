## Improvement on Bellman Ford

```py
def improved_bellman_ford(G, w, s): # O(V+E)
    vertices = topo_sort(G) # O(V)
    for u in vertices:
        for v in G.neighbours[u]: # O(E)
            relax(u, v, w)
```

## Dijkstra's Algorithm

This is a faster algo to solve the single source shortest path problem when $w:E \to \mathbb{R}^{+}$


```py
def dijkstras(G, w, s):
    init_graph(G, s) # O(V)
    visited = set()
    min_heap = G.V
    while len(min_heap) > 0: # O(V)
        u = extract_min(min_heap) # O(log V)
        s.add(u)
        for v in G.neighbours[u]: # O(E)
            relax(u, v, w) # requires the use of decrease_key() !! # O(log V)
```

