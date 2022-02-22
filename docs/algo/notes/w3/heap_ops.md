## Max Heapify

```py
def max_heapify(a: list[int], i: int, hs: int = None) -> None:
    if not hs:
        hs = len(a)

    l = 2*i+1
    r = 2*i+2
    if a[l] > a[r]:
        if l < hs and a[l] > a[i]:
            a[l], a[i] = a[i], a[l]
            max_heapify(a, l, hs)
    else:
        if r < hs and a[r] > a[i]:
            a[r], a[i] = a[i], a[r]
            max_heapify(a, l, hs)
    
```

$\mathcal{O}(\log n)$

## Build Max Heap

```py
def build_max_heap(a: list[int]) -> None:
    for i in range(hs//2)[::-1]:
        max_heapfiy(a, i)
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

$\mathcal{O} \log n$