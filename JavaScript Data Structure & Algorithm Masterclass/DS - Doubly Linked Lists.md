| Instructor | Institution | Course | Lecture |
|: --- :|: --- :|: --- :|: --- :|
| Colt Steele | Udemy | Data Structure & Algorithm | Data Structures |

![[DLL.png]]

### Big O
| Insertion | Removal | Searching | Access |
|: --- :|: --- :|: --- :|: --- :|
| $O(1)$| $O(1)$ | $O(n)$ | $O(n)$ |

> Note: Indexing counts as a separate operation from insertion or removal. Inserting or removing a node in reality consists of getting to the particular node (searching) and then performing the said action.

> Technically, searching in doubly linked lists is $O(n/2)$ thanks to the decreased total number of nodes visited, but on broader terms it's still considered $O(n)$.

### Data Structure
**Node**
```js
class Node {
    constructor(value, next = null, prev = null) {
        this.value = value;
        this.next = next;
        this.prev = prev;
    }
}
```

**Doubly Linked List**
```js
class DoublyLinkedList {
    constructor() {
        this.head = null;
        this.tail = null;
        this.length = 0;
    }
}
```
**Doubly Linked List -- Push**
```js
push(value) {
	const newNode = new Node(value);
	if (!this.length) {
		this.head = newNode;
		this.tail = newNode;
	} else {
		this.tail.next = newNode;
		newNode.prev = this.tail;
		this.tail = newNode;
	}
	this.length ++;
	return this;
}
```
**Doubly Linked List -- Pop**
```js
pop() {
	const poppedNode = this.tail;

	if (!this.length) {
		return undefined;
	} else if (this.length === 1) {
		this.head = null;
		this.tail = null;
	} else {
		this.tail = this.tail.prev;
	}
	this.length --;
	return poppedNode;
}
```
**Doubly Linked List -- Traverse**
```js
traverse() {
	if (!this.length) return undefined;
	let currentNode = this.head;
	do {
		console.log(currentNode.value);
		currentNode = currentNode.next;
	} while (currentNode)
}
```
**Doubly Linked List -- Shift**
```js
shift() {
	if (!this.length) return undefined;
	const shiftedNode = this.head;
	if (this.length === 1) {
		this.head = null;
		this.tail = null;
	} else {
		this.head = this.head.next;
		this.head.prev = null;
	}
	this.length --;
	return shiftedNode;
}
```
**Doubly Linked List -- Unshift**
```js
unshift(value) {
	const newNode = new Node(value);
	if (!this.length) {
		this.head = newNode;
		this.tail = newNode;
	} else {
		this.head.prev = newNode;
		newNode.next = this.head;
		this.head = newNode;
	}
	this.length++;
	return this;
}
```

**Doubly Linked List -- Get**
```js
get(i) {
	if (i >= this.length || i < 0) return undefined;
	if (this.length === 1) return this.head;
	if (i < Math.floor(this.length / 2)) {
		// go from left;
		let node = this.head;
		while (i > 0) {
			node = node.next;
			i--;
		}
		return node;
	} else {
		// go from right;
		let node = this.tail;
		while ((this.length - i - 1) > 0){
			node = node.prev;
			i++;
		}
		return node;
	}
}
```
**Doubly Linked List -- Set**
```js
set(i, value) {
	const node = this.get(i);
	if (node) {
		node.value = value;
		return true;
	}
	return false;
}
```

**Doubly Linked List -- Insert**
```js
insert(i, value) {
	if (i < 0 || i > this.length) return false;
	if (i === this.length) {
		// end of list, or empty list;
		this.push(value);
	} else if (i === 0) {
		this.unshift(value);
	} else {
		const oringinNode = this.get(i);
		const newNode = new Node(value);
		newNode.next = oringinNode;
		newNode.prev = oringinNode.prev;
		oringinNode.prev.next = newNode;
		oringinNode.prev = newNode;
		this.length++;
	}
	return true;
}
```

**Doubly Linked List -- Remove**
```js
remove(i) {
	if (!this.length || i < 0 || i >= this.length) return null;
	if (i === 0) {
		return this.shift();
	} else if (i === this.length - 1) {
		return this.pop();
	} else {
		const removeNode = this.get(i);
		removeNode.prev.next = removeNode.next;
		removeNode.next.prev = removeNode.prev;
		this.length--;
		return removeNode;
	}
}
```