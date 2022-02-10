## Complexities Of Common Sorting Algos

Bubble, Insertion, Selection: $O(n^2)$

Heap, Merge, Quick: $O(n log \; n)$

## Certain Technicalities With Solving Recurrances:

1. In practice, we assume that $T(n) = \Theta(1)$
2. We assume that $n$ is divisible by the denominator in recurrance relations. $\left\lfloor \cfrac{n}{2} \right\rfloor$ is not required.

The reason why these can be neglected is because they do not influence the order of growth asymptotically.

The different methods to solve recursion are:

1. By expansion
2. By substitution
3. [Master Theorem](../master_peak "Master Theorem & Peak Finding")