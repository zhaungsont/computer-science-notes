**Resources**
- [JavaScript.Info - Event loop: microtasks and macrotasks](https://javascript.info/event-loop)
- [PJCHENder - Event loop, micro-task, macro-task, async JavaScript](https://pjchender.dev/javascript/note-event-loop-microtask/)

![[Event Loop.png]]

### Definitions
- **Macrotasks** are newly loaded scripts, events, and `setTimeout`s.
- **Microtasks** are promises: executions of `then/catch/finally` or `await`.

### Event Loop Algorithm
1.  Dequeue and run the oldest task from the _macrotask_ queue (e.g. “script”).
2.  Execute **all** _microtasks_:
    -   While the microtask queue is not empty:
        -   Dequeue and run the oldest microtask.
3.  Render changes if any.
4.  If the macrotask queue is empty, wait till a macrotask appears.
5.  Go to step 1.

### Rules
- Microtask queue 和 macrotask queue 是分開獨立紀錄的。
- Async function 中的**第一個 await code 本身是 synchronous 的**，第一個 await 之後的程式會被排到 microtask queue
- Promise 中，**到 then 之前的都是 synchronous，then 之後的才是 async**。
