## What is a Hash Table
- Hash tables are used to store **key-value** pairs.
	- Input: "`I love cats`", output: "`1099842588`"
- Hash tables hold an **unordered** collection of data.
- Hash tables are **fast ($O(1)$) for getting, adding, and removing items**.
- (Some kind of) Implementations of hash tables in programming languages:
	- Python: Dictionaries
	- JavaScript: Objects, Maps
	- Java, Go, Scala: Maps
	- Ruby: Hashes

## Hash Function
Hash function is the way to convert keys into valid array indices.


### Extra: Write a Hash Function in JavaScript
From [this stackoverflow post](https://stackoverflow.com/questions/7616461/generate-a-hash-from-string-in-javascript)
```javascript
String.prototype.hashCode = function() {
  var hash = 0,
    i, chr;
  if (this.length === 0) return hash;
  for (i = 0; i < this.length; i++) {
    chr = this.charCodeAt(i);
    hash = ((hash << 5) - hash) + chr;
    hash |= 0; // Convert to 32bit integer
  }
  return hash;
}

const str = 'revenue'
console.log(str, str.hashCode())
```

Here's another one:
```javascript
const cyrb53 = (str, seed = 0) => {
    let h1 = 0xdeadbeef ^ seed, h2 = 0x41c6ce57 ^ seed;
    for(let i = 0, ch; i < str.length; i++) {
        ch = str.charCodeAt(i);
        h1 = Math.imul(h1 ^ ch, 2654435761);
        h2 = Math.imul(h2 ^ ch, 1597334677);
    }
    h1  = Math.imul(h1 ^ (h1 >>> 16), 2246822507);
    h1 ^= Math.imul(h2 ^ (h2 >>> 13), 3266489909);
    h2  = Math.imul(h2 ^ (h2 >>> 16), 2246822507);
    h2 ^= Math.imul(h1 ^ (h1 >>> 13), 3266489909);
  
    return 4294967296 * (2097151 & h2) + (h1 >>> 0);
};

console.log(`cyrb53('a') -> ${cyrb53('a')}`)
console.log(`cyrb53('b') -> ${cyrb53('b')}`)
console.log(`cyrb53('revenge') -> ${cyrb53('revenge')}`)
console.log(`cyrb53('revenue') -> ${cyrb53('revenue')}`)
console.log(`cyrb53('revenue', 1) -> ${cyrb53('revenue', 1)}`)
console.log(`cyrb53('revenue', 2) -> ${cyrb53('revenue', 2)}`)
console.log(`cyrb53('revenue', 3) -> ${cyrb53('revenue', 3)}`)
```
