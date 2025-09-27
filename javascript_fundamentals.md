# JavaScript Fundamentals and Best Practices

## 1. Data Types in JavaScript

JavaScript supports the following data types: - **Primitive types**:
String, Number, Boolean, Null, Undefined, Symbol, BigInt -
**Non-primitive types**: Objects, Arrays, Functions

## 2. Variable Declarations: `let`, `const`, and `var`

-   **`let`**: Block-scoped, can be reassigned, not hoisted like `var`.
-   **`const`**: Block-scoped, cannot be reassigned (immutable binding).
-   **`var`**: Function-scoped, hoisted with undefined initialization.

### Why Not Use `var`?

`var` often leads to bugs because it is **function-scoped**, not
block-scoped. Hoisting also causes unexpected behavior.

## 3. Why Global Variables Are Bad

-   Pollute the global namespace.
-   Can be unintentionally overwritten.
-   Lead to hard-to-debug code.

## 4. Truthy and Falsy Values

-   **Falsy values**: `false`, `0`, `""`, `null`, `undefined`, `NaN`
-   **Truthy values**: Everything else.

## 5. Function Hoisting

-   Function declarations are hoisted.
-   Function expressions and arrow functions are **not** hoisted.

## 6. Functions Without Return Statement

A function without a return statement returns **`undefined`**.

## 7. Ways of Declaring Functions

-   Function declaration: `function myFunc() {}`
-   Function expression: `const myFunc = function() {}`
-   Arrow function: `const myFunc = () => {}`

## 8. Pass by Reference vs Pass by Value

-   **Primitive types**: Passed by value.
-   **Objects/arrays**: Passed by reference.

## 9. For Loops in JavaScript

-   `for (let i = 0; i < n; i++)` -- Numeric iteration.
-   `for..in` -- Iterates over object keys.
-   `for..of` -- Iterates over iterable values.
-   `forEach` -- Array method for iteration.

## 10. Searching on MDN

Always refer to [MDN Docs](https://developer.mozilla.org/) for
up-to-date JavaScript references.

## 11. Popular Array Utility Methods

-   `map`, `filter`, `reduce`, `forEach`, `find`, `some`, `every`,
    `sort`, `concat`, `slice`, `splice`

## 12. Popular String Utility Methods

-   `toUpperCase`, `toLowerCase`, `includes`, `substring`, `slice`,
    `split`, `replace`, `trim`

## 13. Popular Object Utility Methods

-   `Object.keys`, `Object.values`, `Object.entries`, `Object.assign`,
    `Object.freeze`, `Object.seal`

## 14. When to Use `forEach` vs `map`, `filter`, `reduce`

-   Use `forEach` for side effects (logging, modifying external
    variables).
-   Use `map`, `filter`, `reduce` when **transforming data**.

## 15. Immutable vs Mutable Methods

-   **Immutable**: `map`, `filter`, `concat`, `slice`
-   **Mutable**: `push`, `pop`, `shift`, `splice`, `sort`

## 16. Error Handling

-   **try...catch** is used to handle errors gracefully.
-   **throwing errors** stops execution.

### Throwing Errors

``` js
throw new Error("Error message"); // Best practice
throw "Error message"; // Not recommended
```

## 17. Reading Error Messages

-   Error messages include the **type of error**, message, and **stack
    trace**.
-   Practice reading stack traces daily.

## 18. Importance of Catch Block

Prevents application crashes by handling exceptions safely.

## 19. Spread Operator

Expands arrays or objects:

``` js
const arr = [1, 2, 3];
const newArr = [...arr, 4, 5];
```

## 20. Template Literals

Use backticks `` ` `` for string interpolation:

``` js
const name = "JS";
console.log(`Hello, ${name}`);
```

## 21. Default Parameters

``` js
function greet(name = "Guest") {
  console.log("Hello " + name);
}
```

## 22. Destructuring

``` js
const {a, b} = {a: 1, b: 2};
```

## 23. Closures

A closure is when a function "remembers" variables from its outer scope
even after execution.

## 24. Arrow Functions vs Regular Functions

-   Arrow functions don't have their own `this`.
-   Regular functions bind `this` dynamically.

## 25. Strict Equality vs Loose Equality

-   `===` checks value and type.
-   `==` performs type coercion.

## 26. Why `value === undefined` is Better

`!value` fails for falsy values like `0`, `""`. Explicit check avoids
bugs.

## 27. Array Utility Method Chaining

``` js
const result = arr.filter(x => x > 2).map(x => x * 2).reduce((a, b) => a + b, 0);
```

## 28. Null vs Undefined

-   `null`: Explicit absence of value.
-   `undefined`: Declared but not assigned.

## 29. Modules

``` js
// export
module.exports = myFunc;

// import
const myFunc = require("./myFunc");
```

## 30. Console Methods

-   `console.log()` -- Standard logging
-   `console.error()` -- Error logging
-   `console.info()` -- Informational logs
-   `console.table()` -- Tabular data

## 31. Best Practices

-   Consistent **indentation**.
-   Meaningful **variable names**.
-   Avoid reusing loop variables.
-   Keep functions small and reusable.

## 32. Passing Functions to Other Functions

``` js
function greet(fn) {
  fn("Hello");
}
greet(console.log);
```

## 33. Named vs Anonymous Functions

-   **Named**: Easier debugging in stack traces.
-   **Anonymous**: Useful for short inline callbacks.

## 34. Variable Number of Arguments

``` js
function sum(...nums) {
  return nums.reduce((a, b) => a + b, 0);
}
```
