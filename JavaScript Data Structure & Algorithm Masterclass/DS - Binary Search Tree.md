| Instructor  | Institution | Course                     | Lecture         |
| : --- :     | : --- :     | : --- :                    | : --- :         |
| Colt Steele | Udemy       | Data Structure & Algorithm | Data Structures |

## Big O
| Insertion | Searching |
|: --- :|: --- :|
| $O(log\ n)$| $O(log\ n)$|

## Data Structure
**Node**
```js
class Node {
    constructor(value) {
        this.value = value;
        this.left = null;
        this.right = null;
    }
}
```

**Binary Search Tree**
```js
class BinarySearchTree {
    constructor() {
        this.root = null;
    }
}
```

**Insert**
```js
insert(value) {
	const newNode = new Node(value);
	if (!this.root) {
		this.root = newNode;
	} else {
		let prevNode = this.root;
		let thisNode = this.root;
		while (thisNode) {
			prevNode = thisNode;
			if (value < thisNode.value) {
				// go left
				thisNode = thisNode.left;
			} else {
				// go right
				thisNode = thisNode.right;
			}
		}
		if (value < prevNode.value) {
			prevNode.left = newNode;
		} else {
			prevNode.right = newNode;
		}
		
	}
}
```

**Find** 
```js
find(value){
	if(!this.root) return false;
	
	let node = this.root;
	while (node.value !== value){
		if(value < node.value){
			if (!node.left) return false;
			node = node.left;
		} else {
			if (!node.right) return false;
			node = node.right;
		}
	}
	return node;
}

```

## Tree Traversal
- [[Algo - Tree Traversal]]