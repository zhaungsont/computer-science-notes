**Resources**
- [Temporal Dead Zones (TDZ)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#temporal_dead_zone_tdz)
**Prerequisites**
- [[Hoisting]]

A `let` or `const` variable is said to be in a "temporal dead zone" (TDZ) from the start of the block until code execution reaches the line where the variable is **declared and initialized**.

## TDZ: This is Where This Value is Undeclared or Uninitialized
While inside the TDZ, the variable has not been initialized with a value, and any attempt to access it will result in a [`ReferenceError`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ReferenceError). The variable is initialized with a value when execution reaches the line of code where it was declared. This differs from [`var`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var#var_hoisting) variables, which will return a value of `undefined` if they are accessed before they are declared.

```js
{
  // TDZ starts at beginning of scope
  console.log(bar); // undefined
  console.log(foo); // ReferenceError
  var bar = 1;
  let foo = 2; // End of TDZ (for foo)
}
```


## The Zoning Depends on *When* the Variable Has a Value
The term "temporal" is used because the zone depends on the order of execution (time) rather than the order in which the code is written (position). For example, the code below works because, even though the function that uses the `let` variable appears before the variable is declared, the function is _called_ outside the TDZ.

```js
{
  // TDZ starts at beginning of scope
  const func = () => console.log(letVar); // OK

  // Within the TDZ letVar access throws `ReferenceError`

  let letVar = 3; // End of TDZ (for letVar)
  func(); // Called outside TDZ!
}
```

> It's is not about **where** we'll reach TDZ, but **when**.

