**Resources**
- [Hoisting (MDN)](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)

JavaScript **Hoisting** refers to the process whereby the interpreter *appears* to move the _declaration_ of **functions**, **variables** or **classes** to the top of their scope, prior to execution of the code.

**_Hoisting_ is not a term normatively defined in the ECMAScript specification.**

## Types of Hoisting

In colloquial terms, any of the following behaviors may be regarded as hoisting:

1.  Being able to use a variable's value in its scope before the line it is declared. ("Value hoisting")
2.  Being able to reference a variable in its scope before the line it is declared, without throwing a [`ReferenceError`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ReferenceError), but the value is always [`undefined`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined). ("Declaration hoisting")
3.  The declaration of the variable causes behavior changes in its scope before the line in which it is declared.

|     | Definition                                                                                                                                                                         | 中文定義                                                                                  | Instance |
|:---:| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | --- |
|  1  | Being able to use a variable's value in its scope before the line it is declared. ("Value hoisting")                                                                               | 在變數宣告前就可引用它的值                                                                | `function` & `async function`    |
|  2  | Being able to reference a variable in its scope before the line it is declared, without throwing a `ReferenceError`, but the value is always `undefined`. ("Declaration hoisting") | 可以在一個變數的作用域內引用該變數，而不會導致 `ReferenceError`，但該值會是 `undefined`。 | `var`    |
|  3  | The declaration of the variable causes behavior changes in its scope before the line in which it is declared.                                                                      | WTF                                                                                         |  `let`, `const`, and `class`   |


### The Term "Hoisting" is Disputed, but Not Baseless
Some prefer to see `let`, `const`, and `class` as non-hoisting, because the [temporal dead zone](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#temporal_dead_zone_tdz) strictly forbids any use of the variable before its declaration. However, the temporal dead zone can cause other observable changes in its scope, which suggests there's some form of hoisting:

```js
const x = 1;
{
  console.log(x); // ReferenceError
  const x = 2;
}
```

>When [`let`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let) or [`const`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const) variables are accessed before the line in which they are declared is executed, a [`ReferenceError`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ReferenceError) is thrown.

Still, it may be more useful to characterize lexical declarations as **non-hoisting**, because from a utilitarian perspective, the **hoisting of these declarations doesn't bring any meaningful features**.



**See also**
- [[Temporal Dead Zones]]
- [[Declaration vs. Initialization]]
- [ReferenceError: can't access lexical declaration 'X' before initialization (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Cant_access_lexical_declaration_before_init)
