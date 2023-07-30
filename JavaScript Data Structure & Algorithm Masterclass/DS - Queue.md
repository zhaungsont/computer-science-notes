| Instructor | Institution | Course | Lecture |
|: --- :|: --- :|: --- :|: --- :|
| Colt Steele | Udemy | Data Structure & Algorithm | Data Structures |

### Intro
A Queue is defined as a linear data structure that is open at both ends and the operations are performed in **First In First Out (FIFO) order**.

### Big O
| Insertion | Removal | Searching | Access |
|: --- :|: --- :|: --- :|: --- :|
| $O(1)$| $O(1)$| $O(n)$ | $O(n)$ |

## Data Structure
**Node**
```js
class Node {
    constructor (value) {
        this.value = value;
        this.next = null;
    }
}
```
**Queue**
```js
class Queue {
    constructor () {
        this.first = null;
        this.last = null;
        this.length = 0;
    }

    enqueue(value) {
        const newNode = new Node(value);
        if (!this.length) {
            this.first = newNode;
            this.last = newNode;
        } else {
            this.last.next = newNode;
            this.last = newNode;
        }
        this.length++;
        return this.length;
    }

    dequeue() {
        if (!this.length) return undefined;
        const removedNode = this.first;

        if (this.length === 1) {
            this.first = null;
            this.last = null;
        } else {
            this.first = removedNode.next;
        }

        this.length --;
        return removedNode.value;
    }
}
```