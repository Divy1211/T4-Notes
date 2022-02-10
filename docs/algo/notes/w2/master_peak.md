## Master Theorem

Let $a, b > 0$, $f(n)$ an asymptotically positive funciton, and $T(n)$ a recurrance relation defined on the positive integers

$T(n) = aT(n/b) + f(n)$

1. If $f(n) = \mathcal{O}(n^{\textstyle log_b \; a - \epsilon})$ for some $\epsilon > 0$ then $T(n) = \Theta(n^{\textstyle log_b \; a})$
2. If $f(n) = \Theta(n^{\textstyle log_b \; a})$ then $T(n) = \Theta(n^{\textstyle log_b \; a} log n)$
3. If $f(n) = \Omega(n^{\textstyle log_b \; a + \epsilon})$ for some $\epsilon > 0$ and if $a f(n/b) \leq cf(n)$ for some constant $c < 1$ and all sufficiently large $n$, then $T(n) = \Theta(f(n))$


These cases are however, not exhaustive. For example, it is possible for $f(n)$ to be asymptotically larger than $n^{\textstyle log_b a}$, but not larger by a polynomial factor (no matter how small the exponent in the polynomial is). For example, this is true when $f(n) = n^{\textstyle log_b a} log \; n$. In this situation, the master theorem would not apply!

## Peak Finding

1. In 1D: This refers to the problem of finding a number in an array such that it is greater than all (max 2, min 1) of its neighbours
2. In 2D: This refers to the problem of finding a number in a 2D array such that it is greater than all (max 4, min 2) of its neighbours

Divide and conquer is used to solve this, and the time complexity:

1D: $\mathcal{O}(log \; n)$

2D: $\mathcal{O}(nlog \; n)$