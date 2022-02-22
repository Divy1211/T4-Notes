## Property

In a BST, the following two properties must hold:

1. The nodes in the left sub tree of a given node must be $\leq$ to itself
2. The nodes in the right sub tree of a given node must be $\geq$ to itself

## Traversal

1. In order: $LR_oR$
2. Pre order: $R_oLR$
3. Post order: $LRR_o$

## Operations

1. `tree_insert` $\mathcal{O}(\log n)$

    ```py
    def find_parent(T, x):
        current = T.root
        while current:
            if x.key < current.key and current.left:
                current = current.left
            elif current.right:
                current = current.right

        return current


    def tree_insert(T, x):
        y = find_parent(T, x)
        x.parent = y
        if not T.root
            T.root = x
            return
        if x.key < y.key:
            y.left = x
        else:
            y.right = x
    ```

2. `tree_delete` $\mathcal{O}(\log n)$
    ```py
    def tree_delete(T, x):
        if not x.left and not x.right:
            del x
            return

        if not x.left or not x.right:
            x = x.left or x.right:
            return

        y = tree_min(x.right) # the smallest element in the right subtree is still bigger than all elements in x's left sub tree but also less than or equal to all elements in the right subtree of x by definition.

        y.parent.left = y.right
        y.left = x.left
        y.right = x.right

        x = y    
    ```


3. `tree_max` $\mathcal{O}(\log n)$

    ```py
    def tree_max(x):
        if not x:
            return None

        current = x
        while current.right:
            current = current.right
    ```

4. `tree_min` $\mathcal{O}(\log n)$

    ```py
    def tree_min(x):
        if not x:
            return None

        current = x
        while current.left:
            current = current.left
    ```

5. `tree_search` $\mathcal{O}(\log n)$

    ```py
    def tree_search(x, k):
        current = x

        while current and current.key != k:
            if k < current.key:
                current = current.left
            else:
                current = current.right

        return current

    ```

6. `successor` $\mathcal{O}(\log n)$

    ```py
    def succ(x):
        if x.right:
            return tree_min(x.right)

        y = x.parent
        while y and x == y.right: # if you are the right most element of your subtree, then your successor is the right child of the closest ancestor node whoes left sub tree you are in
            x = y
            y = y.parent

        return y
    ```


7. `predecessor` $\mathcal{O}(\log n)$

    ```py
    def predec(x):
        if x.left:
            return tree_max(x.left)

        y = x.parent
        while y and x == y.left: # if you are the left most element of your subtree, then your predecessor is the closesnt ancestor node whoes right sub tree you are in
            x = y
            y = y.parent
            
        return y
    ```