Since all the operations' complexities depend on the height of a node in the BST, it is good to minimise the height as much as possible. Thus, we come up with the concept of a "self-balancing" AVL tree.

## What is an AVL Tree

An AVL tree is a tree that satisfies the balanced height property. We say that the tree is height-balanced

1. In this tree, each node has an additional attribute: `#! py x.height`. If `#!py x is None`, `x.height := -1`
2. This is a tree such that the heights of the left and the right subtrees of each node differ by at most 1. This is known as the balance height property. (This is the same as the tree being *nearly complete*)

The height of an AVL tree with $n$ nodes is $\left\lfloor \log n \right\rfloor$

1. A node of a BST is **left-heavy** if the height of the left subtree is > height of the right subtree + 1
2. A node of a BST is **right-heavy** if the height of the right subtree is > height of the left subtree + 1

## Operations

### Left Rotate
This is performed on a node which is right heavy
```py
def left_rotate(B):
    parent = B.parent
    if B is parent.right:
        parent.right = B.right
        B.right = B.right.left
        parent.right.left = B
    elif B is parent.left:
        parent.left = B.right
        B.right = B.right.left
        parent.left.left = B
```

### Right Rotate
This is performed on a node which is left heavy
```py
def right_rotate(B):
    parent = B.parent
    if B is parent.right:
        parent.right = B.left
        B.left = B.left.right
        parent.right.right = B
    elif B is parent.left:
        parent.left = B.left
        B.left = B.left.right
        parent.left.right = B
```

### Double Left (Right Left) Rotate
This is performed on a node which is right heavy and the right sub tree itself is left heavy
```py
def double_left_rotate(A):
    right_rotate(A.right)
    left_rotate(A)
```

### Double Right (Left Right) Rotate
This is performed on a node which is left heavy and the left sub tree itself is right heavy
```py
def double_right_rotate(A):
    left_rotate(A.left)
    right_rotate()
```