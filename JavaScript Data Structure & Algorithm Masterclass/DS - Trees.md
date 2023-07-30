## Introduction
![[tree.png]]

### Definition
A tree is a type of data structure where one node (parent) can point to multiple other nodes (children) to represent or simulate hierarchy. 
- There must be a single entry point, aka **root**.
- All the nodes must point **downwards**; pointing to sibling(s) or parent(s) is not allowed.

### Terminology
- **Root**: the starting node.
- **Parent**: a node that directly points to another node(s) downward; a **child** is the converse notion of it.
- **Siblings**: a group of nodes with the same parent.
- **Leaf**: a node with no children.
- **Edge**: the connection between one node and another.

### Tree v.s. Linked Lists
The main difference between a tree and a linked list is that a linked list is **linear**.
> Note that linked lists *are* a kind of tree.

# Binary Search Trees
Binary search trees are a type of binary tree, which is a type of tree.
Binary search trees are used for data sorting, usually in numbers.
- Every parent node has **at most** two children.
- **Every node to the left of a parent node is always less than the parent.**
- **Every node to the right of a parent node is always greater than the parent.**
![[BSTSearch.png]]


## Operations on Binary Search Trees
- [[DS - Binary Search Tree]]
- [[DS - Binary Heaps]]
- [[Algo - Tree Traversal]]
