

# DSA (JavaScript)
| Instructor | Institution | Course | Lecture |
|: --- :|: --- :|: --- :|: --- :|
| Colt Steele | Udemy | Data Structure & Algorithm | Big O |

# Big O

## Time Complexity

### Omit the Constants（常數）

- $O(n + 1)$ → $O(n)$
- $O(5n)$ → $O(n)$
- $O(n^2 + 5n + 1)$ → $O(n^2 + n)$ㄐ

### Time Spent on Assignments, Operations, & More

- **Arithmetic operations are constant**
    - $2 + 2$ takes roughly the same time as $1,000,000,000 + 2$.
- **Variable assignment is constant**
    - `let x = 2;` takes about as long as `let x = 1000000000;`.
- **Accessing elements in an array (by index) or object (by key) is constant**
- **In a loop, the time complexity is:**

$$
length\ of\ loop\ \times\ complexity\ of\ operations\ inside\ loop
$$

### Chart of Time Complexity
![[time complexity.png]]

### What’s the Time Complexity?

1. logAtMost10
    
    ```jsx
    function logAtMost10(n) {
        for (var i = 1; i <= Math.min(n, 10); i++) {
            console.log(i);
        }
    }
    ```
    
    <aside>
    💬 As `n` increases, the operation of the function `logAtMost10` stays at 10 steps, which is constant, therefore we can conclude that the time complexity of this function is **O(1)**.
    
    </aside>
    
2. logAtLeast10
    
    ```jsx
    function logAtLeast10(n) {
        for (var i = 1; i <= Math.max(n, 10); i++) {
            console.log(i);
        }
    }
    ```
    
    <aside>
    💬 As `n` increases, the operation of the function `logAtLeast10` increases to `n` steps, therefore we can conclude that the time complexity of this function is **O(n)**.
    
    </aside>
    

### Misc: Formula for Finding the Sum of $1...n$

$$
S_n = n\ (n + 1)\ /\ 2
$$

This is far, far better than incrementing the numbers in a for loop, which has the time complexity of $O(n)$.

## Space Complexity

### Big Word: Auxiliary Space & Space Complexity

<aside>
📌 ***Auxiliary Space* is the extra space or temporary space used by an algorithm.**

</aside>

<aside>
📌 ***The space Complexity* of an algorithm is the total space taken by the algorithm with respect to the input size. Space complexity includes both Auxiliary space and space used by input.**

</aside>

### (Auxiliary) Space Complexity of Data Types

- Most primitives (booleans, numbers, `undefined`, `null`) are **constant space**.
    - `var x = 1` and `var y = 100_000_000` can be considered taking up the same space in memory.
- **Strings require $O(n)$ space, where $n$ is the string length**
    - `var s = "abcdefghij"` can be considered taking up 10x more space than `var s2 = "a"`.
- **Reference types** are generally $O(n)$, where $n$ is the **array length** or **number of keys in an object.**

| Data Types | (Auxiliary) Space Complextiy | (n) being |
| --- | --- | --- |
| Most Primitives (boolean, Number, undefined, null) | O(1) | N/A |
| Strings | O(n) | Length of string |
| Arrays | O(n) | Length of array |
| Objects | O(n) | Number of keys |

### Identifying Space Complexity

```jsx
function sum(arr){
	**let total = 0;**
	for (**let i = 0;** i < arr.length; i++){
		total += arr[i];
	}
	return total;
}
```

```jsx
**Auxiliary Space Complexity:

total: number;
i: number;**

```

<aside>
📌 We created **two** variables in the entirety of this function. We did not add even more variables based off of the length of the input array; the space complexity of this function remains $O(n)$.

</aside>

## Big O of Objects

**JavaScript Objects are unordered data collections in key-value pairs. They are efficient in fast access, insertion, and removal — the time complexity of doing them is $O(1)$.**

| Operation | Definition | Time Complexity |
| --- | --- | --- |
| Insertion | Adding something to an object. | O(1) |
| Removal | Deleting something in an object. | O(1) |
| Searching | Checking to see if a given piece of information is in a value of a certain item. 
We will need to potentially search every single item to find the value we are looking for. | O(n) |
| Access | Retrieving something with a key from an object. | O(1) |

### Big O of Object Methods

| Method | Description | Time Complexity |
| --- | --- | --- |
| Object.keys() | Loops through an object and returns an array of all the keys inside it. | O(n) |
| Object.values() | Loops through an object and returns an array of all the values inside it. | O(n) |
| Object.entries() | Loops through an object and returns an array of all the key-value pairs inside it. | O(n) |
| Object.hasOwnProperty() | Checks with a key to see if a property exists on an object. Time complexity is constant time because we can quickly access all object properties with keys. | O(1) |

## Big O of Arrays

| Operation | Definition | Time Complexity |
| --- | --- | --- |
| Insertion |  |  |
| Removal |  |  |
| Searching |  | O(n) |
| Access | Retrieving a value from an array  with index. | O(1) |

## Recursions
As opposed to **iteration**, recursion calls upon itself and **can sometime be a cleaner alternative**. 

### Recursion Usage
- `JSON.parse` / `JSON.stringify`.
- `document.getElementById` and DOM traversal algorithms.
- Object traversal.
- In more complex data structures.

### How It Works
Recursive functions invoke itself (with different inputs) until it reaches the **base case, i.e., the condition when the recursion end**.


