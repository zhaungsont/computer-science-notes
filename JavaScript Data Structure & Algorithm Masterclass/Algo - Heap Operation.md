![[heap_indexing_find_children.jpg]]
![[heap_indexing_find_parent.jpg]]

## Insert (Max)

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


## Extract (Max)
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


## See Also
- [[Algo - Priority Queue]]