| Instructor | Institution | Course | Lecture |
|: --- :|: --- :|: --- :|: --- :|
| Colt Steele | Udemy | Data Structure & Algorithm | Searching Algorithms |

## Linear Search
**Time Complexity**
Best case: $O(1)$
Worst case: $O(n)$
Avg. case: $O(n)$

**Built-in JS Functions that Utilize Linear Search**
- indexOf
- includes
- find
- findIndex

**Code Snippet**
```js
function linearSearch(arr, val) {
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] === val) return i;
    }

    return -1;
}

linearSearch([9, 8, 7, 6, 5, 4, 3, 2, 1, 0], 10) // -1
```

---
## Binary Search
**Time Complexity**
Best case: $O(1)$
Worst case: $O(log\ n)$
Avg. case: $O(log\ n)$

**Requirements**
- Input array must be sorted (high-to-low or low-to-high for numbers, alphabetical string-wise)

**Code Snippet**
```js
function binarySearch(arr, value) {
    let left = 0;
    let right = arr.length - 1;
    
    while (true){
        if (right < left) return -1
        let pointer = Math.floor((right + left) / 2);
        
        if (arr[pointer] === value) {
            return pointer;
        } else if (arr[pointer] < value) {
            left = pointer + 1;
        } else {
            right = pointer - 1;
        }
    }
}

binarySearch([5, 6, 10, 13, 34, 35, 37, 40, 44, 86], 10) // 2
```

---
## Naive String Search

**Code Snippet**
```js
function naiveStringSearch(str, word) {
    let matchCount = 0;
    for (let i = 0; i < str.length; i++) {
        if (str[i] === word[0]) {
            // inner loop
            let matched = true;
            for (let j = 1; j < word.length; j++) {
                if (word[j] !== str[i + j]) {
                    matched = false;
                    break;
                }
            }
            if (matched) matchCount++;
        }
    }
    return matchCount;
}

const str = 'abcdebbcdfg';
const word = 'bcd'

naiveStringSearch(str, word) // 2
```

```js
// Approach #2
function naiveStringSearch(str, word) {
	let count = 0;
	for (let i = 0; i < str.length; i++) {
		for (let j = 0; j < word.length; j ++) {
			if (word[j] !== str[i+j]) {
				break;
			}
			if (j === word.length -1) {
				count++;
			}
		}
	}
	return count;
}

const str = 'abcdebbcdfg';
const word = 'bcd'

naiveStringSearch(str, word) // 2
```
