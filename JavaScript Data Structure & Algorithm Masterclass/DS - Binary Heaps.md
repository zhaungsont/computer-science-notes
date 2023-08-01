> In [computer science](https://en.wikipedia.org/wiki/Computer_science "Computer science"), a **heap** is a specialized [tree](https://en.wikipedia.org/wiki/Tree_(data_structure) "Tree (data structure)")-based [data structure](https://en.wikipedia.org/wiki/Data_structure "Data structure") that satisfies the **heap property**: In a _max heap_, for any given [node](https://en.wikipedia.org/wiki/Node_(computer_science) "Node (computer science)") C, if P is a parent node of C, then the _key_ (the _value_) of P is greater than or equal to the key of C. In a _min heap_, the key of P is less than or equal to the key of C. The node at the "top" of the heap (with no parents) is called the _root_ node.

# Variants of Heap
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

# Binary Heap
- Each parent has at most **two child nodes**.
- The value of each parent node is **always** greater/less than its child nodes.
- In a max Binary Heap the parent is greater than the children, but there are no guarantees between sibling nodes. (No Implied Ordering Between Siblings)
- **A binary heap is as compact as possible**. All the children of each node are as full as they can be and left children are filled out first. 

**Max Binary Heap**
![[Binary_heap.svg]]

**Min Binary Heap**
![[min_binary_heap.png]]

## Operations on Binary Heap

![[heap_indexing_find_children.jpg]]
![[heap_indexing_find_parent.jpg]]

### Insert (Max)

**Instructor's Solution**
```js
class MaxBinaryHeap {
    constructor() {
        this.values = [];
    }
	    
    insert(value) {
        this.values.push(value);
        this.bubbleUp(); // helper function
    }
		
    bubbleUp() {
        let idx = this.values.length - 1;
        const element = this.values[idx];
        while (idx > 0) {
            let parentIdx = Math.floor((idx - 1) / 2);
            let parent = this.values[parentIdx];
			
            if (element <= parent) break;
			
            this.values[parentIdx] = element;
            this.values[idx] = parent;
            idx = parentIdx;
        }
    }
}
```

**My Solution (potentially more inefficient)**
```js
class MaxBinaryHeap {
    constructor() {
        this.values = [];
    }
		
    insert(value) {
        if (!this.values.length) {
            this.values.push(value);
        } else {
            this.values.push(value);
            let thisNodeIdx = this.values.length - 1;
            let parentNodeIdx = Math.floor((thisNodeIdx - 1) / 2);
            
            while (this.values[thisNodeIdx] > this.values[parentNodeIdx]) {
                // swap
                const tmp = this.values[thisNodeIdx];
                this.values[thisNodeIdx] = this.values[parentNodeIdx];
                this.values[parentNodeIdx] = tmp;
				
                thisNodeIdx = parentNodeIdx;
                parentNodeIdx = Math.floor((thisNodeIdx - 1) / 2);
            }
        }
    }
}
```


### Extract (Max)
The **extract** operation removes the root from the heap, restructures the heap, and finally returns the extracted root.

**Instructor's Solution**
```js
extractMax() {
	const max = this.values[0];
	const end = this.values.pop();
	if (this.values.length > 0) {
		this.values[0] = end;
		this.sinkDown();
	}
	return max;
}

sinkDown() {
	let idx = 0;
	const length = this.values.length;
	const element = this.values[0];
	while (true) {
		let leftChildIdx = 2 * idx + 1;
		let rightChildIdx = 2 * idx + 2;
		let leftChild, rightChild;
		let swap = null;
		
		if (leftChildIdx < length) {
			leftChild = this.values[leftChildIdx];
			if (leftChild > element) {
				swap = leftChildIdx;
			}
		}
		if (rightChildIdx < length) {
			rightChild = this.values[rightChildIdx];
			if (swap === null && rightChild > element || swap !== null && rightChild > leftChild) {
				swap = rightChildIdx;
			}
		}
			
		if (swap === null) break;
		this.values[idx] = this.values[swap];
		this.values[swap] = element;
		idx = swap;
	}
}

```

**My Solution**
it's broken :(

## Priority Queue
> In [computer science](https://en.wikipedia.org/wiki/Computer_science "Computer science"), a **priority queue** is an [abstract data-type](https://en.wikipedia.org/wiki/Abstract_data_type "Abstract data type") similar to a regular [queue](https://en.wikipedia.org/wiki/Queue_(abstract_data_type) "Queue (abstract data type)") or [stack](https://en.wikipedia.org/wiki/Stack_(abstract_data_type) "Stack (abstract data type)") data structure. Each element in a priority queue has an associated _priority._
> -- Wikipeida

In our implementation, each node consists of a ***value*** storing the info of this task, and more importantly the ***priority*** value which the PriorityQueue will use to determine where this node will be placed in a queue.

This Priority Queue is also a **Min Binary Heap**, where the lower the value of a node has, the higher it will be allocated.

```js
class Node {
    constructor(value, priority) {
        this.value = value;
        this.priority = priority;
    }
}

class PriorityQueue {
    constructor() {
        this.values = [];
    }

    enqueue(value, priority) {
        const newNode = new Node(value, priority);
        this.values.push(newNode);
        this.bubbleUp();
    }

    bubbleUp() {
        let idx = this.values.length - 1;
        const element = this.values[idx];
        while (idx > 0) {
            let parentIdx = Math.floor((idx - 1) / 2);
            let parent = this.values[parentIdx];

            if (element.priority >= parent.priority) break;

            this.values[parentIdx] = element;
            this.values[idx] = parent;
            idx = parentIdx;
        }
    }

    dequeue() {
    	const min = this.values[0];
    	const end = this.values.pop();
    	if (this.values.length > 0) {
    		this.values[0] = end;
    		this.sinkDown();
    	}
    	return min;
    }

    sinkDown() {
    	let idx = 0;
    	const length = this.values.length;
    	const element = this.values[0];
    	while (true) {
    		let leftChildIdx = 2 * idx + 1;
    		let rightChildIdx = 2 * idx + 2;
    		let leftChild, rightChild;
    		let swap = null;
    		
    		if (leftChildIdx < length) {
    			leftChild = this.values[leftChildIdx];
    			if (leftChild.priority < element.priority) {
    				swap = leftChildIdx;
    			}
    		}
    		if (rightChildIdx < length) {
    			rightChild = this.values[rightChildIdx];
    			if (swap === null && rightChild.priority < element.priority || swap !== null && rightChild.priority < leftChild.priority) {
    				swap = rightChildIdx;
    			}
    		}
    			
    		if (swap === null) break;
    		this.values[idx] = this.values[swap];
    		this.values[swap] = element;
    		idx = swap;
    	}
    }
}

const ER = new PriorityQueue();
ER.enqueue('common cold', 3);
ER.enqueue('concussion', 2);
ER.enqueue('gunshot wound', 1);
ER.enqueue('head expolded', 0);
ER.enqueue('stomach ache', 3);
ER.enqueue('artery cut', 1);
ER.enqueue('ligma', 0);
ER.enqueue('balls', 0);

/*
PriorityQueue {values: Array(8)}
{
    "values": [
        {
            "value": "head expolded",
            "priority": 0
        },
        {
            "value": "balls",
            "priority": 0
        },
        {
            "value": "ligma",
            "priority": 0
        },
        {
            "value": "gunshot wound",
            "priority": 1
        },
        {
            "value": "stomach ache",
            "priority": 3
        },
        {
            "value": "concussion",
            "priority": 2
        },
        {
            "value": "artery cut",
            "priority": 1
        },
        {
            "value": "common cold",
            "priority": 3
        }
    ]
}
*
```

# Time Complexity of Binary Heaps
![[binary_heap_time_complexity.jpg]]
Insertion: $O(log\ n)$ (usual & worst case)
Removal: $O(log\ n)$ (usual & worst case)
Search: $O(n)$
