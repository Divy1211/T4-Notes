## Problem Definition

Document D: A string of chars, raw input.

An array of words Dwords: An array of words as they appear in D

Word Dict W: A map of words to their frequencies in the doc.

Notation: D(w) = frequency of w in D.

## Algorithm

A document is treated like a vector, and the dot product of the vectors is computed to determine the similarity score. Dot product is defined as if two positions in document have same word +1.

Then, we normalise the dot prod with the lengths.

We can also measure the distance by finding the angle between the vectors