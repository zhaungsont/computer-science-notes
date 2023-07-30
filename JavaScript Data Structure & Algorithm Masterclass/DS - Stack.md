| Instructor | Institution | Course | Lecture |
|: --- :|: --- :|: --- :|: --- :|
| Colt Steele | Udemy | Data Structure & Algorithm | Data Structures |

### Intro
Stacks in Data Structures is a linear type of data structure that follows the **LIFO (Last-In-First-Out) principle** and allows insertion and deletion operations from one end of the stack data structure, that is top.

### Big O
| Insertion | Removal | Searching | Access |
|: --- :|: --- :|: --- :|: --- :|
| $O(1)$| $O(1)$| $O(n)$ | $O(n)$ |

### Data Structure
**Node**
```js
class Node {
    constructor (value) {
        this.value = value;
        this.next = null;
    }
}
```

**Stack**
```js
class Stack {
    constructor () {
        this.first = null;
        this.last = null;
        this.length = 0;
    }

    push(value) {
        const newNode = new Node(value);

        newNode.next = this.first;
        this.first = newNode;
        if (!this.length) this.last = newNode;
        this.length ++;
        return this.length;
    }

    pop() {
        if (!this.length) return undefined;
        const removedNode = this.first;
        if (this.length === 1) {
            this.first = null;
            this.last = null;
        } else {
            this.first = this.first.next;
        }

        this.length--;
        return removedNode.value;
    }
}
```