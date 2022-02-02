## What is an Algo?

An algo is any well defined computational procedure that takes a set of values as an input and performs some action or produces a set of values as an output. It is a sequence of steps that transform the input.

A finite procedure for solving a computational problem. This can be described in flow charts, english, or pseudo code.

Incorrect algorithms - that don't give the correct output for some inputs. They are useful when their error rates can be controlled.

Algo Efficiency: The resources needed to run the algo on a computer. These include **time**, **memory** and **hardware**.

## What is a Computational Problem?

Maps an input to an output. Like a function. Has an **input space**, an **output space**

**input instance**: A particular input from the input space. T(n) is the exact number of steps needed (in the worst case scenario) to finish an algo.

## Measures of asymptotic complexity

$\Theta$ - "grows =", grows as fast as...

$\mathcal{O}$ - "grows <=", grows at most as fast as...

$\Omega$ - "grows >=", grows at least as fast as...

$0.1n^2 - 100n^{1.9} + 5 = \Theta(n^2) \implies$ as $n \to \infty$ The left side grows as fast as $n^2$
$n^10 - 100n^{1.9} + 5 = \Omega(n^2) \implies$ as $n \to \infty$ The left side grows at least as fast as $n^2$
$0.1n^2 - 100n^{1.9} + 5 = \mathcal{O}(n^3) \implies$ as $n \to \infty$ The left side grows at most as fast as $n^3$

Exact Definitions:

$f(n) = \mathcal{O}(g(n)) \iff \exists \; D, n_0 > 0 \; | \; f(n) \leq Dg(n) \; \forall \; n \geq n_0$
$f(n) = \Omega(g(n)) \iff \exists \; D, n_0 > 0 \; | \; f(n) \geq Dg(n) \; \forall \; n \geq n_0$
$f(n) = \Theta(g(n)) \iff \exists \; D_1, D_2, n_0 > 0 \; | \; D_1g(n) \leq f(n) \leq D_2g(n) \; \forall \; n \geq n_0$

$f(n) = \Omega(g(n)) \; \& \; f(n) = \mathcal{O}(g(n)) \iff f(n) = \Theta(g(n))$