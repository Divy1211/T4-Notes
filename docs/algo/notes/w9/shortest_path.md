## Graph Theory Terminology

A graph $G$ consists of a set of vertices $V$, and a set of edges $E$. Common notation to describe all 3 together: $G(V, E)$

### DiGraph
A **directed** graph is a graph whos edges are **ordered** pairs of vertices, i.e. $(u, v)$ is different from $(v, u)$.

An edge $(u, v)$ means that an edge going from $u$ to $v$. Here, $u, v \in V$.

$u$ - also referred to as the tail

$v$ - also referred to as the head

### UndiGraph

An **undirected** graph is a graph whos edges are **unordered** pairs of vertices, i.e. $\{u, v\}$ is the same as $\{v, u\}$. Here, $u, v \in V$.

A **simple** graph is one with no self loops/multiple edges connecting the same two nodes.

A **weighted** graph is one where each edge is assigned a numerical weight

### Terms related to vertices and edges

$e = (u, v)$ (Diag) or $e = \{u, v\}$ (Undiag)

Then we have:

$u$ is **incident** to $e$

$v$ is **incident** to $e$

A vertex is **isolated** if it is not incident to any edge

If two vertices are incident to the same edge, then they are **adjacent** or **neighbours**. Adjacency is commutative.

### Incidence List

An **incidence list** is a *hash table* with $n$ slots where each slot is a *linked list* (i.e. collisons resolved by chaining)

Each slot corresponds to some vertex $v$ and the linked list in that slot consists of *all the edges incident to v*. (undirected graphs)

For directed graphs, there is on more condition on the above, i.e. for an edge to be in the linked list of a vertex, the vertex must be at the tail of that edge as well

### Incidence Matrix

If the graph has $n$ vertices and $m$ edges, then this is an $n \times m$ matrix $M$ where the rows correspond to each vertex and the columns correspond to each edge.

For an undirected graph, if a vertex is incident to an edge then the column for that edge has a 1 for both the rows of the corresponding vertices

For a directed graph, the tail vertex has a $-1$ entry instead


### Adjacency List

An **adjacency list** is a *hash table* with $n$ slots where each slot is a *linked list* (i.e. collisons resolved by chaining)

Each slot corresponds to some vertex $v$ and the linked list in that slot consists of *all the vertices adjacent to v*. (undirected graphs)

For directed graphs, the head vertex does not have the reference of the tail vertex in its linked list.

In other words, the linked list only consists of the vertices adjacent to $v$ for which $v$ is the tail of the edge connecting the two

### Adjacency Matrix

If the graph has $n$ vertices, then this is an $n \times n$ matrix $M$ where the rows and columns both correspond to the vertices of the graph.

For undirected graphs, a (row, column) entry in the matrix is 1 if the two corresponding vertices are adjacent. Always symmetric

For directed graphs, a (row, column) entry in the matrix is 1 if the two corresponding vertices are adjacent and the row vertex is the tail of the edge connecting the two

### Path

A **path** in a graph is a sequence of edges such that every two consecutive edges in the sequence are incident to a common vertex.

### Cycle

A **cycle** in a graph is a path such that the first and the last edges are incident to a common vertex

### A Path from one vertex to another

If the common vertex is distinct for each consecutive pair of edges in the path, then the path is simple. If the first edge is incident to $v$ and the last vertex is incident to $u$ then we can say that there is a **path from vertex $v$ to $u$**

A path may also just be represented as a sequence of vertices

### Weight Function

If the graph $G(V, E)$ is weighted, then there is a **weight function** $w: E \to \mathbb{R}$.

common notation: $w(e) or w(u, v)$

The weight of a path $p$ can be described as the sum of all the weights of the edges contained in the path. $w(p)$


## The Shortest Path Problem

Given a directed graph $G(V, E)$, a weight function $w: E \to \mathbb{R}$, and two nodes $u$ and $v$ find the path $p$ connecting the two such that $w(p)$ is minimum. $\delta(u, v)$ is called the smallest path weight from $u$ to $v$. $\delta(u, v) = w(p)$ for the shortest path $p$

If the graph contains a cycle, then there are two possibilities:

1. The cycle has a net positive weight sum => there is only one shortest path between the nodes
2. The cycle has a net negative weight sum => there is no shortest path between the nodes! $\delta(u, v) := -\infty$ in this case

Cycles in shortest paths:

1. If $p$ has a positive weight cycle, then it cannot be the shortest path because we can just remove the cycle and get an even shorter path (contradiction!).
2. If $p$ has a $0$ weight cycle, then it can be **a** shotest path (not unique)

Subpaths of a shortest path are also shortest paths! This is because if they were not, we could replace them in the original shortest path to get an even shorter path (contradiction!)

Thus, we have the following results (Triangle Inequalities):

1. For any vertex $x$ in the shortest path, $\delta(u, v) = \delta(u, x) + \delta(x, v)$
2. For any vertex $x'$ in the shortest path, $\delta(u, v) \leq \delta(u, x') + \delta(x', v)$

Consequently, if $(u, v)$ is a directed edge then:

1. $\delta(s, v) \leq \delta(s, u) + w(u, v)$ (If the shortest path to a node is through $u$ the equality holds, if the shortest path is not through $u$ then the $<$ case must hold. If it doesn't then its not the shortest path!)

## Single Source Shortest Path Problem

Given a directed graph $G(V, E)$, a weight function $w: E \to \mathbb{R}$, and a node $s$, find a shortest path from $s$ to every other vertex in $G$!