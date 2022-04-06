## Common DP Problems

### Knapsack Prolem

### Rod Cutting Problem

### Text Justification Problem

$\text{cost} = \sum\limits_{\text{all lines}} (\text{extra space chars in line})^2$

Supports distributing the extra spaces accross the lines
larger spaces cost more than many small spaces

Inputs:

1. A string of text `text` with $n$ words of varying lengths
2. Each line must have a fixed width $w$

```py
# number of characters neede to wtrite words i to j of text (w/ spaces)
def length(text, i, j):
    ls = text.split(" ")
    total_length = -1

    for k in range(i, j):
        total_length += len(ls[k])+1

    return max(total_lengths, 0)

# additional cost in our cost function due to number of extra spaces
def line_cost(text, i, j, w):
    l = length(text, i, j)
    
    return sys.maxsize if l > w else (w-l)**2
```

$DP[i]$ = min cost from word $i$
Original Problem = $DP[0]$

Recurrance = $DP[i] = min(line\_cost(i, j), DP[j]) \; \forall \; j \in \{i+1, i+2, ..., n\}$

#### Bottom Up Approach
Order for solving DP can be determined using toposort.

```py
def justified_align(text, w):
    n = len(text.split(" "))

    DP = [(w-length(text, i, i+1))**2 for i in range(n+1)]

    for i in range(n-1, -1 -1):
        DP[i] = min([line_cost(text, i, j, w) + DP[j] for j in range(i+1, n+1) ])
    
    return DP[0]
```

#### Top Down Up Approach
Order for solving DP can be determined using toposort.

```py
memo = {}
def justified_align_r(text, w, i = 0):

    if i in memo:
        return memo[i]

    n = len(text.split(" "))
    if i == n:
        memo[i] = (w-length(text, n, n+1))**2
        return memo[i]
    
    memo[i] =  min([line_cost(text, i, j, w) + justified_align_r(text, w, j) for j in range(i+1, n+1) ])
    return memo[i]
```

### Matrix Chain Parenthesization Problem

Given $n$ matrices $M_1, ..., M_n$ such that the product $\prod\limits_{i=1}^{n} M_i$ is well defined ($M_i$ commutes with $M_{i+1}$) determine the minimum number of scalar multiplications needed to compute the product.

If $AB$ where $A$ is $m \times n$ and $B$ is $n \times o$ then the multiplications needed is $mno$

If $ABC$ where $A$ is $n \times 1$ where $B$ is $1 \times n$ and $C$ is $n \times 1$, computing $A(BC)$ is faster than $(AB)C$

So an order of optimum multiplication needs to be determined!

For $\prod\limits_{i=1}^{n}M_i$ to be well defined, the dimesions be: $p_0, p_1, ..., p_n$.

A martix $M_i$ has dim $p_{i-1} \times p_i$

let $c[i,j] = \text{min cost for} \prod\limits_{k=i}^{j}M_k$ computed over all possible paranthesizations

The original problem is therefore: $c[1, n]$

Recurrance: $c[i, j] = min(c[i, k] + c[k+1, j] + p_{i-1}p_{k}p_{j}) \; \forall \; k \in \{i, i+1, ... j-1\}$ where $i < j$

#### Bottom Up Approach

```py
def mat_chain_paren(p):
    n = len(p)-1

    c = [[0]*(n) for _ in range(n)]
    
    for i in range(n-2, -1, -1):
        for j in range(i+1, n):
            c[i][j] = min([c[i][k] + c[k+1][j] + p[i]p[k+1]p[j+1]])
    
    return c[0, n-1]
```

#### Top Down Approach

```py
memo = {}
def mat_chain_paren_r(p, i = 0, j = -1):
    n = len(p)-1

    if j == -1:
        j = n-1

    if (i, j) in memo:
        return memo[i, j]

    if i == j:
        memo[i, j] = 0
        return 0
    
    memo[i, j] = min([mat_chain_paren_r(p, i, k) + mat_chain_paren_r(p, k+1, j) + p[i]p[k+1]p[j+1]])
    
    return memo[i, j]
```

### Longest Common Subsequence

#### Bottom Up Approach

```py
def lcs(X, Y):
    
    X = tuple(X)
    Y = tuple(Y)

    DP = [[()]*len(Y) for _ in range(len(X))]

    for i in range(len(X)):
        for j in range(len(Y)):
            if X[i] == Y[i]:
                DP[i][j] = DP[i-1][j-1]+(X[-1],)
                continue

            if len(DP[i-1][j]) >= len(DP[i][j-1]):
                DP[i][j] = DP[i-1][j]
                continue
            DP[i][j] = DP[i][j-1]

    return DP[len(X)-1][len(Y)-1]
```

#### Top Down Approach
```py
memo = {}
def lcs(X, Y):

    X = tuple(X)
    Y = tuple(Y)

    if len(X) == 0 or len(Y) == 0:
        memo[X, y] = ()
        return ()

    if X[-1] == Y[-1]:
        memo[X, Y] =  lcs(X[:-1], Y[:-1])+(X[-1],)
        return memo[X, Y]
    
    sub_i = lcs(X[:-1], Y)
    sub_j = lcs(X, Y[:-1])

    if len(sub_i) >= len(sub_j):
        memo[X, Y] = sub_i
        return sub_i

    memo[X, Y] = sub_j
    return sub_j
```

## Bottom Up vs Top Down

If all sub problems must be solved once, BU is better because less initialisation and recursion overhead

If not all sub problems need to be solved though, top down approach is better because then we only solve those problems which require solving