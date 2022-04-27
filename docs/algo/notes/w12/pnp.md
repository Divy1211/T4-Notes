## Tractable problem

A problem that can be solved in polynomial time

## Intractable problem

An intractable problem cannot be solved in polynomial time (guaranteed that no polynomial time soln exists for such a problem)

## Unsolvable problems

Halting Problem

## Optimisation problems

Want to find the best soln of a problem given some input and constraints on that input. Eg: sssp, lcs, knapsack, travelling salesman

## Decision problems

Given a candidate soln for an optimisation problem, determine if it is an actual soln. An algo to verify an answer is called a verification algorithm. An answer that satisfies the decision problem is called a certificate

## Verification Algorithms

An algorithm to verify an answer is known as a verification algorithm. Two types of verification algorithms:

1. One that verifies that a "YES" answer is correct,
2. and one that verifies if a "NO" answer is correct.
   
A verification algorithm takes in two inputs $I$ and $E$

1. $I$ is the given input to the decision problem,
2. $E$ represents evidence that we provide to the algorithm. If $E$ is sufficient evidence then hte algorithm outputs `1` and we say that $E$ is a **certificate** for the verification algorithm

## Non Deterministic Algorithm

Is one which may have different outputs even for the same input

## NP

A decision problem is said to be in class NP if there is at least one non deterministic P time algorithm that is able to verify a yes answer to the decision problem such that in the best case scenario this non deterministic algorithm runs in polynomial time

A decision problem is in NP if for every input whoes corresponding correct answer should be yes, there is a certificate for that yes answer that can be verified in polynomial time

## Polynomial Time Reduction

If we can show that a solution to problem A can be derived from a solution to problem B, we can say that we have reduced problem A to problem B.

This reduction comprises two algorithms $F$ and $F^{-1}$

$F$: An algorithm to transforms an input for $A$ to an input for $B$.

$F^{-1}$: An algorithm to transform a solution for $B$ to a solution for $A$.

The reduction is called a polynomial-time reduction if both algorithms $F$ and $F^{-1}$ run in polynomial time

A problem **B** is NP Hard if every NP problem has a polynomial time reduction to **B**

A problem is NP Complete if it is both NP Hard and in NP. 3-SAT.

If we show that a problem **B** is a polynomial time reduction of another NP hard problem, then by definition **B** is also NP Hard! (because transitively every problem in NP can thus be reduced to **B**)

## Hamiltonian path problem

Crosses each vertex exactly once

Given a simple graph $G$, is there a Hamiltonian path in $G$?

## Hamiltonian cycle problem

Given a simple graph $G$, is there a Hamiltonian cycle in $G$?

## Reducing HCP to TSP

### 1. Inputs:

HCP: $G = (V, E)$

TSP: $G' = (V, E')$ where $w(e)$ is defined $\forall \; e \in E'$

### 2. Procedure F

$w(e) := 1 \; \forall \; e \in E$

$w(e) := \infty \; \forall \; e \notin E$

Number of ways to select a pair of vertices from $V$ is $\displaystyle\binom{|V|}{2}$ = $\cfrac{|V|(|V|-1)}{2}$

Therefore, $\mathcal{O}(|V|^2)$

### 3. Outputs

TSP: $p = {e_1, e_2, ..., e_n}$ where $e_1$ and $e_n$ is incident to a common vertex

HCP: yes/no depending on if there is an HCP in $G$

### 4. Procedure $F^{-1}$

if $w(p) = \infty$ then NO else YES. $\mathcal{O}(1)$

## Notation

$A \leq_p B$ means that there is a P time reduction from A to B

$A \cong_p B$ means that $A \leq_p B$ and $B \leq_p C$

## HCP $\cong_p$ HPP

---

## K Colouring

$k$-colouring is an assignemnt of colours from a set of $k$ colours to the nodes of a graph such that no two adjacent nodes have the same colour.

### Vertex colouring problem

is a graph $G$, $k$-colourable? NP-Complete, 3-colouring problem is also NP complete. 3-SAT problem is also NP-Complete

## Clique

A clique is a subset of vertices in a graph that are pairwise adjacent. A $k$-clique is a clique of $k$ vertices

Finding if a graph has a $k$ clique is an NP complete problem

## Independent set

An independent set is a subset of vertices in a graph such that no two vertices are pairwise adjacent. A $k$-independent set is an independent set with $k$ vertices

Finding if a graph has a $k$ independent set is an NP complete problem

## Vertex cover

A vertex cover is a subset of vertices in a graph such that every edge in the graph is incident to at least one edge. A $k$-vertex cover is a vertex cover with $k$ vertices

Finding if a graph has a $k$ vertex cover is an NP complete problem

## Undecidable problems

aka Unsolvable problems. There are uncountably infinite undecidable problems