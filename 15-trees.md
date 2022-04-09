# Trees

This will cover Binary Trees, Binary Search Trees, and K-ary Trees. 

## Common Terminology
- `Node` - A Tree node is a component which may contain its own values, and references to other nodes
- `Root` - The root is the node at the beginning of the tree
- `K` - A number that specifies the maximum number of children any node may have in a k-ary tree. In a binary tree, k = 2.
- `Left` - A reference to one child node, in a binary tree
- `Right` - A reference to the other child node, in a binary tree
- `Edge` - The edge in a tree is the link between a parent and child node
- `Leaf` - A leaf is a node that does not have any children
- `Height` - The height of a tree is the number of edges from the root to the furthest leaf

## Depth First
Depth first traversal is where we prioritize going through the depth (height) of the tree first. There are multiple ways to carry out depth first traversal, and each method changes the order in which we search/print the root. Here are three methods for depth first traversal:

- Pre-order: root >> left >> right
- In-order: left >> root >> right
- Post-order: left >> right >> root

The most common way to traverse through a tree is to use recursion. With these traversals, we rely on the call stack to navigate back up the tree when we have reached the end of a sub-path.

### Pre-order
Let’s break down the pre-order traversal. Here is the pseudocode for this traversal method:

```
ALGORITHM preOrder(root)
OUTPUT <-- root.value

  if root.left is not NULL
      preOrder(root.left)

  if root.right is not NULL
      preOrder(root.right)
```

Pre-order means that the root has to be looked at first. In our case, looking at the root just means that we output its value. When we call preOrder for the first time, the root will be added to the call stack:

Next, we start reading our preOrder function’s code from top to bottom. This means that we will output the root.value out to the console. Then, our next block of code instructs us to check if our root has a left node set. If the root does, we will then send the left node to our preOrder method recursively. This means that we make another function call, where B is our new root, and so on untell it finish the left. Then tha same implements to the right untill the tree finishes.

### In-order

```
ALGORITHM inOrder(root)
// INPUT <-- root node
// OUTPUT <-- in-order output of tree node's values

    if root.left is not NULL
        inOrder(root.left)

    OUTPUT <-- root.value

    if root.right is not NULL
        inOrder(root.right)
```


### Post-order

```
ALGORITHM postOrder(root)
// INPUT <-- root node
// OUTPUT <-- post-order output of tree node's values

    if root.left is not NULL
        postOrder(root.left)

    if root.right is not NULL
        postOrder(root.right)

    OUTPUT <-- root.value
```

<br>

## Breadth First



<br>

## K-ary Trees



<br>

## Binary Search Trees



<br>

[Reference](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-15/resources/Trees.html)