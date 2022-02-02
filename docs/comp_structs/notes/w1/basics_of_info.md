## Definitions

**Information** is defined as knowledge communicated or received concerning a particular fact or circumstance.

**Encoding** is the process of assigning representations to information. Strings of bits can mean some value of integers, but we can also assign a fixed repesentation to them.

**Decoding** is the process of mapping bits to their assigned representations to retrieve encoded information.

ASCII (Fixed Length), UTF-8 (Variable Length)

**Fixed Length Encoding**: Assigning an equal length of bits to all choices when they are equally probable.

## Information and Probability

The amount of information held by an event is inversly proportional to the probability of it happening. (Information is thus proportional to the uncertainty of an event happening)

If there are $n$ discrete events $x_i$ with each having a probability of occuring as $p_i$ then the number of bits needed to find out exactly which event happpened is given by $I(X) = log_2 \cfrac{1}{p_i}$

For instance, if there are 256 possible characters that can appear in an ASCII encoded text document, with each character being equally likely (untrue for actual text documents) to occurr, $log_2\cfrac{1}{1/256} = 8$ bits are needed to find out the character at a given position in the document.

### Narrowing Down Choices

If we go from having $N$ equally likely choices to $M$ equally likely choices, ($N > M$) we can then say that we were given $log_2 \cfrac{N}{M}$ bits of information.

For example, if we learn that the first bit of a character in an ASCII encoded text document is `1`, then we go from having 256 choices for characters to 128. This is exactly what the formula tells us: $log_2 \cfrac{256}{128} = 1$