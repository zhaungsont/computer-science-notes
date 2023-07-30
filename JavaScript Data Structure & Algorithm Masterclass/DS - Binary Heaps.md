> In [computer science](https://en.wikipedia.org/wiki/Computer_science "Computer science"), a **heap** is a specialized [tree](https://en.wikipedia.org/wiki/Tree_(data_structure) "Tree (data structure)")-based [data structure](https://en.wikipedia.org/wiki/Data_structure "Data structure") that satisfies the **heap property**: In a _max heap_, for any given [node](https://en.wikipedia.org/wiki/Node_(computer_science) "Node (computer science)") C, if P is a parent node of C, then the _key_ (the _value_) of P is greater than or equal to the key of C. In a _min heap_, the key of P is less than or equal to the key of C. The node at the "top" of the heap (with no parents) is called the _root_ node.

## Variants of Heap
- [2–3 heap](https://en.wikipedia.org/wiki/2%E2%80%933_heap "2–3 heap")
- [B-heap](https://en.wikipedia.org/wiki/B-heap "B-heap")
- [Beap](https://en.wikipedia.org/wiki/Beap "Beap")
- [Binary heap](https://en.wikipedia.org/wiki/Binary_heap "Binary heap")
- [Binomial heap](https://en.wikipedia.org/wiki/Binomial_heap "Binomial heap")
- [Brodal queue](https://en.wikipedia.org/wiki/Brodal_queue "Brodal queue")
- [_d_-ary heap](https://en.wikipedia.org/wiki/D-ary_heap "D-ary heap")
- [Fibonacci heap](https://en.wikipedia.org/wiki/Fibonacci_heap "Fibonacci heap")
- [K-D Heap](https://en.wikipedia.org/wiki/K-D_Heap "K-D Heap")
- [Leaf heap](https://en.wikipedia.org/w/index.php?title=Leaf_heap&action=edit&redlink=1 "Leaf heap (page does not exist)")
- [Leftist heap](https://en.wikipedia.org/wiki/Leftist_tree "Leftist tree")
- [Min-max heap](https://en.wikipedia.org/wiki/Min-max_heap "Min-max heap")
- [Pairing heap](https://en.wikipedia.org/wiki/Pairing_heap "Pairing heap")
- [Radix heap](https://en.wikipedia.org/wiki/Radix_heap "Radix heap")
- [Randomized meldable heap](https://en.wikipedia.org/wiki/Randomized_meldable_heap "Randomized meldable heap")
- [Skew heap](https://en.wikipedia.org/wiki/Skew_heap "Skew heap")
- [Soft heap](https://en.wikipedia.org/wiki/Soft_heap "Soft heap")
- [Ternary heap](https://en.wikipedia.org/wiki/Ternary_heap "Ternary heap")
- [Treap](https://en.wikipedia.org/wiki/Treap "Treap")

## Binary Heap Intro
- Each parent has at most **two child nodes**.
- The value of each parent node is **always** greater/less than its child nodes.
- In a max Binary Heap the parent is greater than the children, but there are no guarantees between sibling nodes. (No Implied Ordering Between Siblings)
- **A binary heap is as compact as possible**. All the children of each node are as full as they can be and left children are filled out first. 

**Max Binary Heap**
![[Binary_heap.svg]]

**Min Binary Heap**
![[min_binary_heap.png]]

## Operations on Binary Heap
- [[Algo - Heap Operation]]
- [[Algo - Priority Queue]]
