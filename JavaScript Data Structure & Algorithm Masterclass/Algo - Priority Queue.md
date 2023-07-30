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

## See also
- [[Algo - Heap Operation]]
- [[DS - Binary Heaps]]
