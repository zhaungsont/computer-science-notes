| Instructor | Institution | Course | Lecture |
|: --- :|: --- :|: --- :|: --- :|
| Colt Steele | Udemy | Data Structure & Algorithm | Sorting Algorithms |


## Introduction

- Depending on the condition of your data sets, different kinds of sorting algorithms can be more efficient or inefficient: **a sorting algorithm can have completely different efficiency sorting a totally random data sets, nearly-sorted data set, reversed data set or a data set with few unique values**.

---


## Build-in JavaScript Sorting Method ([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort))

### `sort`'s Weird Default Behavior

```js
Array.prototype.sort()
```

The array sorting method in JavaScrip might not behave like what we might think. That's because **the default sorting order is according to string Unicode code points**. That means that every time `sort` takes in an array of numbers, **it firsts converts them to strings, before sorting them by the corresponding Unicode code points**.

The `sort` method behaves normally when comparing string arrays.

To combat this unintuitive behavior, we can always pass in a custom function that compares two numbers:

```js
const compareNum = (num1, num2) => num1 - num2;

[4, 2, 3, 1].sort(compareNum)
```

---

## Bubble Sort
**Big O**

| Best case | Worst case | Avg. Case | Space Complexity |
|: --- :|: --- :|: --- :|: --- :|
| $O(n^2)$ | $O(n^2)$ | Data $O(n^2)$ | $O(1)$ |

**Code Snippet**
```js
function bubbleSort(arr) {
    let len = arr.length;
    
    while (len > 1) {
        let allPass = true;
        // check first & second
        for (let i = 0; i < len - 1; i++) {
            if (arr[i] > arr[i + 1]) {
                allPass = false;
                
                const tmp = arr[i];
                arr[i] = arr[i + 1];
                arr[i + 1] = tmp;
            }
        }
        if (allPass) break;
        len--;
		
    }
    
    return arr;
}

bubbleSort([1, 2, 3, 4, 5])
```

---

## Selection Sort
**Big O**

| Best case | Worst case | Avg. Case | Space Complexity |
|: --- :|: --- :|: --- :|: --- :|
| $O(n^2)$ | $O(n^2)$ | Data $O(n^2)$ | $O(1)$ |

**Code Snippet**
```js
function selectionSort(arr) {
    let start = 0;
    
    while (start < arr.length - 1) {
        let smallestIdx = start;
		
        for (let i = start; i < arr.length; i ++){
            if (arr[i] < arr[smallestIdx]) {
                smallestIdx = i;
            }
        }
		
        if (start !== smallestIdx) {
            const tmp = arr[start];
            arr[start] = arr[smallestIdx];
            arr[smallestIdx] = tmp;
            start++;
        }
    }
	
    return arr;
}

const arr1 = [5, 2, 4, 3, 1];
const arr2 = [1, 2, 3, 5, 4];

/**
- loop n - 1 times, with each time starting 1 index further
- in each outer loop, create a var and set it to Infinity
- in each outer loop, start a nested loop that finds the smallest value
- after the nested loop ends, swap the value at the start index of array with the smallest value from the last nested loop
- increment start index

*/


selectionSort(arr1);

```

---

## Insersion Sort
**Big O**

| Best case | Worst case | Avg. Case | Space Complexity |
|: --- :|: --- :|: --- :|: --- :|
| $O(n)$ | $O(n^2)$ | Data $O(n^2)$ | $O(1)$ |

**Code Snippet**
```js
function insertionSort(arr) {
    if (arr.length <= 1) return arr;
    
    for (let i = 1; i < arr.length; i++) {
	    
        let swapIdx = null;
        for (let j = i - 1; j >= 0; j--) {
            console.log('j =', j);
            if (arr[j] > arr[i]) {
                swapIdx = j;
            } else {
                break;
            }
        }
        
        if (swapIdx !== null) {
            const insertValue = arr[i];
            arr.splice(i, 1); // pop that item out of array and re-index.
            arr.splice(swapIdx, 0, insertValue)
        }
    }
    
    return arr;
}

// 1. start outer loop: i = 1; i < arr.length; i ++
// 2. for every outer iteration, check arr[i] against the previous value by starting a nested loop: l = i - 1; l >= 0; l-- (until we reach to the first value in array)
// 3. if there is any value samller, remember the index of it and continue until we find a value that is not smaller, then pull and push the current value to right after that value.
// 4. if there is no value smaller, don't do anything.
// 5. go back to step 2 to another iteration until nested loop ends.
// 6. when outer loop ends, return the mutated array.

insertionSort([1, 2, 3, 6, 5, 4])
```

---

## Comparing Bubble Sort, Selection Sort, & Insertion Sort
- Bubble Sort, Selection Sort, and Insertion Sort are **elementary sorting algorithms**, compared to more advanced ones like merge sort, quick sort, and radix sort.
- They are often called **quadratic sorting algorithms** because the time complexity of all of them is $O(n^2)$.
- For arrays that are **nearly sorted**, Bubble Sort and Insertion Sort can be as fast as near $O(n)$ (but not exactly $O(n)$, that'll need the array to be completely sorted)
	- On the other hand, Selection sort performs poorly even when the array is almost sorted.
- Insersion sort has another strength: if a new element is pushed into the end of the array, it only requires on iteration using insersion sort to place the new element into the the correct index. So insersion sort can also be useful when we want to continue to sort new data as they come in.

---

## Merge Sort

**Big O**

| Best case | Worst case | Avg. Case | Space Complexity |
|: --- :|: --- :|: --- :|: --- :|
| $O(n\ log\ n)$ | $O(n\ log\ n)$ |  $O(n\ log\ n)$ | $O(1)$ |

**Code Snippet**
```js
function mergeSort(arr) {
    const smallArrays = [];
    if (arr.length > 1) {
        const mid = Math.floor(arr.length / 2)
        const leftHalf = arr.slice(0, mid);
        const rightHalf = arr.slice(mid);
        
        return mergeTwoLists(mergeSort(leftHalf), mergeSort(rightHalf));
    } else {
        return arr;
    }
}

function mergeTwoLists(arr1, arr2) {
    if (!arr1.length) return arr2;
    if (!arr2.length) return arr1;

    let idx1 = 0;
    let idx2 = 0;
    let newArr = [];
    while (idx1 < arr1.length && idx2 < arr2.length) {
        if (arr1[idx1] >= arr2[idx2]) {
            newArr.push(arr2[idx2])
            idx2++;
        } else {
            newArr.push(arr1[idx1])
            idx1++;
        }
    }
    if (idx1 === arr1.length) {
        // push the rest in arr2 into newArr
        newArr = newArr.concat(arr2.slice(idx2));
    } else {
        // push the rest in arr1 into newArr
        newArr = newArr.concat(arr1.slice(idx1));
    }
    return newArr;
}
```

---

## Quick Sort

**Big O**

| Best case      | Worst case | Avg. Case      | Space Complexity |
| -------------- | ---------- | -------------- | ---------------- |
| $O(n\ log\ n)$ | $O(n^2)$   | $O(n\ log\ n)$ | $O(1)$           |

**Code Snippet**
```js
const swap = (arr, idx1, idx2) => {
    if (idx1 === idx2) return;

    const tmp = arr[idx1];
    arr[idx1] = arr[idx2];
    arr[idx2] = tmp;
}


function pivotHelper(arr, start = 0, end = arr.length + 1) {

    let pivot = arr[start];
    let swapIdx = start;
    for (let i = start + 1; i < arr.length; i ++) {
        if (pivot > arr[i]) {
            swapIdx++;
            swap(arr, swapIdx, i);
        }
    }
    swap(arr, start, swapIdx);
    return swapIdx;
}

function quickSort(arr, left = 0, right = arr.length - 1) {
    if (left < right) {
        const pivotIdx = pivotHelper(arr, left, right);

        quickSort(arr, left, pivotIdx - 1);
        quickSort(arr, pivotIdx + 1, right);
    }

    return arr;
}

const arr1 = [4, 8, 2, 1, 5, 7, 6, 3]

quickSort(arr1);
```

---

## Radix Sort
**Big O**

| Best case | Worst case | Avg. Case | Space Complexity |
| --------- | ---------- | --------- | ---------------- |
| $O(nk)$   | $O(nk)$    | $O(nk)$   | $O(n + k)$       |
- $n$ is the number of items in the array, and $k$ is the number of digits (length of those numbers).

**Code Snippet**
```js
const radixSort = (arr) => {
	const mostDigit = mostDigits(arr);
	
	for (let i = 0; i < mostDigit; i++) {
		const buckets = Array.from({ length: 10 }, () => []);
		
		arr.forEach((num) => {
			const place = getDigit(num, i);
			buckets[place].push(num);
		});
		
		arr = [].concat(...buckets);
	}
	
	return arr;
};

const getDigit = function (number, idx) {
	return Math.floor((number / Math.pow(10, idx)) % 10);
};

const digitCount = (number) => {
	return number.toString().length;
};

const mostDigits = (arr) => {
	let most = 1;
	
	arr.forEach((number) => {
		const len = digitCount(number);
		
		if (len > most) most = len;
	});
	
	return most;
};

  

radixSort([69, 356, 368, 77, 12, 102, 4, 9]);
```