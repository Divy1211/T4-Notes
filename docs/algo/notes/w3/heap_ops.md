## Max Heapify

```py
def max_heapify(a: list[int], i: int, hs: int = None) -> None:
    if not hs:
        hs = len(a)

    l = 2*i+1
    r = 2*i+2
    max_ = i

    if l < hs and a[max_] < a[l]:
        max_ = l
    if r < hs and a[max_] < a[r]:
        max_ = r

    if max_ != i:
        a[max_], a[i] = a[i], a[max_]
        max_heapify(a, max_, hs)
```

$\mathcal{O}(\log n)$

## Build Max Heap

```py
def build_max_heap(a: list[int]) -> None:
    for i in range(hs//2)[::-1]:
        max_heapify(a, i)
```

$\mathcal{O}(n)$


## Heapsort

```py
def heapsort(a: list[int]) -> None:
    build_max_heap(a)
    for hs in range(len(a))[::-1]:
        a[0], a[hs] = a[hs], a[0]
        max_heapify(a, 0, hs)
```

$\mathcal{O}(n \log n)$

## Extract Max

```py
def extract_max(a: list[int], hs: int = None) -> int:
    if not hs:
        hs = len(a)
    max_ = a[0]
    a[0] = a[hs-1]
    hs -= 1
    max_heapify(a, 0, hs)
    return max_
```

$\mathcal{O} (\log n)$