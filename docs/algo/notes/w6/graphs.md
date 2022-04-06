## What is a Graph

$G = (V, E)$

$V$ is a set of $n$ vertices

$E \subseteq V \times V$ is a set of $m$ edges connecting pairs of vertices.

An edge may have two flavors - Directed/Undirected.

## Ways To Store Graphs
There are three ways to rep a graph:

1. Adjacency Lists ($\mathcal{O}(n+m)$ bits)
2. Incidence Lists (describes an edge $e = (u, v)$, somewhat equivalent to adjacency list)
3. Adjacency Matrix ($\Theta(n^2)$ bits)

1. Add edge: $\mathcal{O}(1)$
2. Check Edge bn Two Vertices: $\mathcal{O}(1)$ for matrix, $\mathcal{O}(n)$ for adj list where $n$ is the number of neighbours
3. Visit All Neighbours: $\Theta(n)$ for matrix, $\mathcal{O}(n)$ for adj list
4. Remove edge: same as check edge.

## Connected Graphs

A graph is connected if there exists a path from any vertex to all other vertices. AKA every pair of vertices is connected

Otherwise, graph is disjoint

## Tree graphs

A connected acyclic graph is known as a tree

A disjoin acyclic graph is called bipartite or a forest

## Minimal Spanning Tree

The minimal spanning tree of a graph is defined as a graph which has the same set of nodes as the original graph, but its edges are a subset of the edges of the original graph. Disjoint graphs do not have MSTs.

## BFS

```py
def bfs(G, s):
    for v in G:
        v. color = "white"
        u.d = sys.maxsize
        u.p = None

    s.color = "gray"
    s.d = 0
    s.p = None

    queue = [s]
    i = 0
    while i < len(queue):
        u = queue[i]
        for v in u.neighbours:
            if v.color == "white":
                v.color = "gray"
                v.d = u.d + 1
                v.p = u
                queue.append(v)
        u.color = black
        i+=1
```

## DFS

```py
time = -1
def dfs(G):
    for v in G:
        v.color = "white"
        u.p = None
    time = 0
    for u in G:
        if u.color == "white":
            dfs_visit(G, u)

def dfs_visit(G, u):
    time += 1
    u.d = time
    u.color = "gray"
    for v in u.neighbours:
        if v.color == "white":
            v.p = u
            dfs_visit(G, v)
    time += 1
    u.f = time
```

Can be used for topo sort

## Predecessor Subgraph

AKA DFS Tree/Forest

$G_p = (V, E_p)$ where
$E_p = \{ (v.p, v) \; | \; v \in V \; \& \; v.p \neq NIL \}$ i.e. all the edges travered during dfs

1. These are known as **Tree Edges**

when going from $u \rightarrow v$

2. **Back Edge** connects a vertex with its ancestor. Self loops in directed graphs count in this. $v.d < u.d < u.f < v.f$
3. **Forward Edge** connects a vertex with its descendent. $u.d < v.d < v.f < u.f$
4. **Cross edges** Any edge that isn't a back, forward or tree edge. $v.d < v.f < u.d < u.flavors$

## Cycle detection
A graph has a cycle iff it has a back edge

## Topo Sort

Run DFS, sort in decreasing order of `v.f`. Used on DAG

Its a linear ordering of all its vertices such that if $u \rightarrow v$ then $u$ appears before $v$ in the ordering.

If the vertices are numbered downward after topo sort, their DFS Tree matrix is an upper triangular matrix


