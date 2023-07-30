![[heap_indexing_find_children.jpg]]
![[heap_indexing_find_parent.jpg]]

## Insert

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


## Extract
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
```js
class MaxBinaryHeap {
    constructor() {
        this.values = [];
    }
		
    extract() {
        if (!this.values.length) return;
        const extracted = this.values[0];
        const tempRoot = this.values.pop();
        let tempRootIdx = 0;
        this.values[0] = tempRoot;
        
        while (true) {
            const child1 = this.values[2 * tempRootIdx + 1];
            const child2 = this.values[2 * tempRootIdx + 2];
            // if any of the child is undefined (out of bound) the condition below wouldn't pass either so it should be fine.
            if (tempRoot < child1 || tempRoot < child2) {
                if (child1 > child2) {
                    // swap left
                    this.values[tempRootIdx] = child1;
                    this.values[2 * tempRootIdx + 1] = tempRoot;
                    tempRootIdx = 2 * tempRootIdx + 1;
                } else {
                    // swap right
                    this.values[tempRootIdx] = child2;
                    this.values[2 * tempRootIdx + 2] = tempRoot;
                    tempRootIdx = 2 * tempRootIdx + 2;
                }
            } else {
                break;
            }
        }
        return extracted;
    }
}
```