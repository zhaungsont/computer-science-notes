| Instructor | Institution | Course | Lecture |
|: --- :|: --- :|: --- :|: --- :|
| Colt Steele | Udemy | Data Structure & Algorithm | Tree Traversal |

> Note: All algorithms listed below are meant to be used in tandem with the tree data structure specified in [[DS - Binary Search Tree]].


![[BFS.png]]

# Breadth First Search

## As a Method of BST
```js
class BST {
	// ... code for BST
	
	BFS() {
		const queue = [this.root];
		const visited = [];
		while (queue.length) {
			const node = queue.shift();
			visited.push(node);
			if (node.left) queue.push(node.left);
			if (node.right) queue.push(node.right);
		}
		return visited;
	}
}
```

## Discrete Function
```js
function BFS(tree) {
    if (!tree.root) return [];
    const queue = [tree.root];
    const visited = [];

    while (queue.length) {
        const thisNode = queue.shift();
        visited.push(thisNode.value);
        if (thisNode.left) queue.push(thisNode.left);
        if (thisNode.right) queue.push(thisNode.right);
    }
    return visited;
}
```


![[DFS.png]]
# Depth First Search

## PreOrder

### Method
```js
DFSPreOrder() {
	const visited = [];
	const current = this.root;
	const traverse = (node) => {
		if (!node) return;
		visited.push(node.value);
		if (node.left) traverse(node.left);
		if (node.right) traverse(node.right);
	}
	traverse(current)
	return visited;
}
```

### Discrete Function
```js
function DFSPreOrder(node) {
    let visited = [];
    console.log('node left', node.left)
    visited.push(node.value)
    if (node.left) visited = visited.concat(DFSPreOrder(node.left));
    if (node.right) visited = visited.concat(DFSPreOrder(node.right));
    console.log('visited', visited)
    return visited;
}
```


## PostOrder

### Method
```js
DFSPostOrder() {
	const visited = [];
	const current = this.root;
	const traverse = (node) => {
		if (!node) return;
		
		if (node.left) traverse(node.left);
		if (node.right) traverse(node.right);
		visited.push(node.value);
	}
	traverse(current)
	return visited;
}
```

### InOrder
```js
DFSInOrder() {
	const visited = [];
	const current = this.root;
	const traverse = (node) => {
		if (!node) return;
		
		if (node.left) traverse(node.left);
		visited.push(node.value);
		if (node.right) traverse(node.right);
	}
	traverse(current)
	return visited;
}
```


# When to Use BFS, When to Use DFS?
- **Time complexity**: when traversing the same tree, using BFS and DFS will always take the same amount of time since both methods go through the entire tree.
- **Space complexity**: BFS and DFS may have a noticeable difference in the space complexity depending on the structure of the tree. Here's why: 
	- The number of nodes in a tree grows exponentially (^2), and the deeper a layer is, the significantly more nodes there are.
	- If the tree is balanced like the example below, our BFS implementation would queue up all the nodes on the same horizontal layer before diving into the next layer. It would look like this:
		```
		queue: [1]
		// queue.shift();
		// queue.push(2, 3);
		
		queue: [2, 3]
		// queue.shift();
		// queue.push(4, 5);
		
		queue: [3, 4, 5]
		// queue.shift();
		// queue.push(6, 7);
		
		queue: [4, 5, 6, 7]
		// queue.shift();
		// queue.push(8, 9);
		
		queue: [5, 6, 7, 8, 9]
		// queue.shift();
		// queue.push(10, 11);
		```
	- The queue in BFS would keep growing until there is no more nodes to push; if a tree has millions of nodes in total, the space complexity of BFS would be drastically higher than that of DFS.

![[tree (large).png]]