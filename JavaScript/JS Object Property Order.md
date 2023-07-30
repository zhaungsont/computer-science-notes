[Stackoverflow Reference](https://stackoverflow.com/questions/5525795/does-javascript-guarantee-object-property-order/38218582#38218582)

## TL; DR
The iteration order for objects follows [a certain set of rules](https://stackoverflow.com/a/38218582/292500) since ES2015, but **it does not (always) follow the insertion order**. Simply put, the iteration order is a combination of the insertion order for strings keys, and ascending order for number-like keys.

## Property Ordering in ES6 Objects
The [order for "own" (non-inherited) properties](https://tc39.es/ecma262/#sec-ordinaryownpropertykeys) is:

1.  Positive integer-like keys in ascending order
2.  String keys in insertion order
3.  Symbols in insertion order

### Example

Given is the following object:

```javascript
const o = Object.create(null, {
  m: {value: function() {}, enumerable: true},
  "2": {value: "2", enumerable: true},
  "b": {value: "b", enumerable: true},
  0: {value: 0, enumerable: true},
  [Symbol()]: {value: "sym", enumerable: true},
  "1": {value: "1", enumerable: true},
  "a": {value: "a", enumerable: true},
});
```

This results in the following order (in certain cases):

```javascript
Object {
  0: 0,
  1: "1",
  2: "2",
  b: "b",
  a: "a",
  m: function() {},
  Symbol(): "sym"
}
```


## Alternatives
Using an array or a [`Map` object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) can be a better way to achieve this. `Map` shares some similarities with `Object` and [guarantees the keys to be iterated in order of insertion](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map#Objects_and_maps_compared), without exception:

> The keys in Map are ordered while keys added to object are not. Thus, when iterating over it, a Map object returns keys in order of insertion. (Note that in the ECMAScript 2015 spec objects do preserve creation order for string and Symbol keys, so traversal of an object with ie only string keys would yield keys in order of insertion)