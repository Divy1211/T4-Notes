## Abstract Data Types

If we do not restrict/specify how certain operations on a data type are implemented, its called an abstract data type (ADT).

It is an abstract mathematical model for objects of a certain datatype together with some defined operations on the objects, where the model does not depend on specific implementations of the operations/programming language

## Data Structure

A data structure (DS) is a format to **store and organise** data in order to facilitate access and modification. Ex: Arrays, List.

A DS can be used to implement an ADT.

The main difference between a DT and a DS is that DS specifies **how/the way** data is stored

## Heaps

A heap is a data structure built from arrays. It is **not** an array!

They can be visualised by a *nearly complete* binary tree. *Nearly complete*: A node cannot have any children until the previous level of nodes **all** have 2 children.

Note that heaps may also be visualised as any general nearly complete *d-ary* (ex. ternary) tree.

Heap properties: Max Heap, Min Heap. A min heap becomes a max heap if we negate all the keys!

1. Depth of a node: length of path from root to node.
2. Depth of the heap: max of all depths in tree (length of path from furthest leaf to root)

.

1. Height of a node: length of path from node to furthest leaf.
2. Height of the heap: max of all heights in tree (length of path from root to furthest leaf)

$Depth = Height = \log_2 n$

1. Parent of $i$: $\left\lfloor \cfrac{i}{2} \right\rfloor$
2. Left Child of $i$: $2i+1$ (for 0 indexed array)
3. Right Child of $i$: $2(i+1)$ (for 0 indexed array)

Operations associated with heaps are called **Heap Operations**.

1. `#!py def build_max_heap`: Build a max-heap from an (unordered) input array. $\mathcal{O}(n)$
2. `#!py def build_max_heapmax_heapify`: $\mathcal{O}(\log n)$
3. `#!py def insert`: $\mathcal{O}(\log n)$
4. `#!py def extract_max`: $\mathcal{O}(\log n)$
5. `#!py def increase_key`: $\mathcal{O}(\log n)$
6. `#!py def heapsort`: $\mathcal{O}(n\log n)$

We can build algos involving these heap operations. Priority Queues: an ADT implemented using heaps

## Priority Queues

A priority queue is an ADT that consists of S set of elements, together with operations on S. Every element of S has an associated key, which is the *priority score* for that element. if $x \in S$ then its key can be denoted by $k(x)$.

The following operations are defined on PQs:

1. `#!py def max(S):` Returns the element with the largest key
2. `#!py def insert(S, x):` Insert an element x into S.
3. `#!py def extract_max(S):` Pop `max(S)`
4. `#!py def increase_key(S, x, k):` Set the key for $x$ to $k$

They are used in:

1. Pathfinding: Dijkstra's algo
2. Targetted advertising: Prim's algorithm
3. Boardband routing management for bandwidth

### Possible Implementations

1. ArrayOrder: Stores elements in the order that they come in
2. ArrayDesc: Sort by decreasing key
3. Heap: Max Heap by key

| Operation           | ArrayOrder       | ArrayDesc              | Heap                  |
| :-----------------: | :--------------: | :--------------------: | :-------------------: |
| `max`               | $\mathcal{O}(n)$ | $\mathcal{O}(1)$       | $\mathcal{O}(1)$      |
| `insert`            | $\mathcal{O}(1)$ | $\mathcal{O}(n)$       | $\mathcal{O}(\log n)$ |
| `extract_max`       | $\mathcal{O}(n)$ | $\mathcal{O}(n)$       | $\mathcal{O}(\log n)$ |
| `increase_key`      | $\mathcal{O}(n)$ | $\mathcal{O}(n)$       | $\mathcal{O}(\log n)$ |
