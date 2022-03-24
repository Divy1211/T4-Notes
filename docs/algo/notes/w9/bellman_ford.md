## Tree

An undirected graph is a tree is it is connected and acyclic

**Acyclic**: no cycles. (=> one and only one path between two vertices)

**Connected**: path from any vertex to any other vertex

A directed graph can be called a tree if its underlying undirected graph is a tree

A tree with $n$ vertices must have $n-1$ edges

## Rooted Tree

A **rooted tree** is a tree with a 'specially distinguished' vertex called the **root** such that for every non rooted $v$ there is exactly one path from root to $v$. A rooted tree can be directed or undirected

If $r$ is the root of a tree then it is said to be **rooted at $r$**

## Constructing the shortest path tree

A shortest path tree of $G$ is a directed graph $G' = (V', E')$ such that:

1. $V' \subseteq V$ and $E' \subseteq E$
2. rooted at vertex $s$. The vertices of $G'$ are all vertices that are reachable from $s$. Due to the tree structure, we know that every path to every node from $s$ is unique and simple, and thus also the shortest path

## Iterative Approach to Estimate $\delta(s, v)$

for all vertices initialise $v.d = \infty$, $s.d = 0$ and $v.p = None$

Then run BFS and update the $v.p$ and $v.d$ if a stricly better $v.d$ is found. Now just follow the $v.p$ chain backwards to get the shortest path

```py
def init_graph(G, s): # O(V)
    for vertex in G:
        v.d = sys.maxsize
        v.p = None
    s.d = 0
```

```py
def relax(u, v, w): # O(1)
    # if the knwon distance to v is longer than the
    # one we are just encountering by exploration, update
    if u.d + w(u, v) < v.d:
        v.d = u.d + w(u, v)
        v.p = u
```

```py
# O(V.E)
def bellman_ford(G, w, s):
    init_graph(G, s) # O(V)

    # main loop for relaxation
    # O(V * E)
    for _ in range(len(G.V)-1):
        for u, v in G.E: # all directed edges
            relax(u, v, w) # O(1)
    
    # O(E)
    # check for negative weight cycles
    for u, v in G.E: # all directed edges
        if v.d > u.d + w.(u, v)
            return False
    return True
```

For this algo to work an order of edges G.E must be specified

Lemma 24.2: if $G$ contains no neg-w cycles reachable from $s$ then after $|V|-1$ iterations of the main loop, we have that $v.d = \delta(s, v)$ for all vertices $v$ of $G$ no matter the order of edges used for relaxation

Theorem 24.4: This algo works. LOL?

Read chapter 24.5 of course txt book.
