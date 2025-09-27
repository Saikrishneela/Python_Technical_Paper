# JavaScript Execution, Async Concepts, Event Loop, and Promises

## 1. How JavaScript Executes Code

JavaScript uses a **single-threaded** model with a **call stack** and
**event loop**.

-   Code is executed line by line (synchronous by default).
-   If it encounters asynchronous tasks (setTimeout, fetch, etc.), they
    are handled by browser APIs or Node APIs.
-   Once the stack is empty, async results are pushed back into the
    stack via the **event loop**.

### Example

``` js
console.log("Start");

setTimeout(() => {
  console.log("Async task done");
}, 1000);

console.log("End");
```

**Output:**

    Start
    End
    Async task done

------------------------------------------------------------------------

## 2. Difference Between Sync & Async

-   **Synchronous**: Code runs line by line, blocking execution until
    finished.
-   **Asynchronous**: Code does not block; tasks are handled in the
    background, results come later.

### Example

``` js
// Synchronous
console.log("1");
console.log("2");
console.log("3");

// Asynchronous
console.log("1");
setTimeout(() => console.log("2 (after 1 sec)"), 1000);
console.log("3");
```

**Output (Async):**

    1
    3
    2 (after 1 sec)

------------------------------------------------------------------------

## 3. Ways to Make Code Async

1.  **Callbacks**
2.  **Promises**
3.  **async/await**

### Callback Example

``` js
function fetchData(callback) {
  setTimeout(() => {
    callback("Data loaded");
  }, 1000);
}

fetchData((msg) => console.log(msg));
```

### Promise Example

``` js
function fetchData() {
  return new Promise((resolve) => {
    setTimeout(() => resolve("Data loaded"), 1000);
  });
}

fetchData().then(msg => console.log(msg));
```

### Async/Await Example

``` js
async function fetchData() {
  return "Data loaded";
}

async function run() {
  const result = await fetchData();
  console.log(result);
}
run();
```

------------------------------------------------------------------------

## 4. What Are Web Browser APIs?

Web APIs are provided by the browser (not JavaScript itself).
Examples: - `setTimeout`, `setInterval` - `fetch` for HTTP requests -
`DOM` APIs (`document.querySelector`, etc.) - `localStorage`,
`sessionStorage`

### Example

``` js
document.body.innerHTML = "<h1>Hello World</h1>";
localStorage.setItem("user", "John");
console.log(localStorage.getItem("user"));
```

------------------------------------------------------------------------

## 5. What Is the Event Loop?

The **event loop** manages the execution of synchronous and asynchronous
tasks.

1.  Executes synchronous code in the call stack.
2.  Sends async tasks to Web APIs.
3.  When async tasks are done, they go into the **callback queue**.
4.  Event loop pushes them back to the call stack when empty.

### Example

``` js
console.log("Start");

setTimeout(() => console.log("Timeout done"), 0);
Promise.resolve().then(() => console.log("Promise resolved"));

console.log("End");
```

**Output:**

    Start
    End
    Promise resolved
    Timeout done

(Promises go to **microtask queue**, which has higher priority than
callback queue.)

------------------------------------------------------------------------

## 6. What Is Callback Hell?

Callback hell happens when multiple async functions are nested, making
code unreadable and hard to maintain.

### Example

``` js
getUser(1, function(user) {
  getPosts(user.id, function(posts) {
    getComments(posts[0].id, function(comments) {
      console.log(comments);
    });
  });
});
```

This is hard to read → solved by **Promises** and **async/await**.

------------------------------------------------------------------------

## 7. What Is Inversion of Control in Callbacks?

When you pass a callback to another function, you give control of
execution to that function.\
This means you cannot fully control **when/how** your callback is
executed.

### Example

``` js
function doTask(callback) {
  // The function decides when to call your callback
  setTimeout(() => {
    callback("Task done");
  }, 1000);
}

doTask((msg) => console.log(msg));
```

Problem: If the API decides **not** to call the callback, your code
won't run as expected.\
Promises fix this by giving you back control.

------------------------------------------------------------------------

# Summary

-   JS is single-threaded, async tasks are handled via event loop.\
-   Sync blocks code, async doesn't.\
-   Async methods: **callbacks, promises, async/await**.\
-   Web APIs handle tasks like timers, fetch, DOM.\
-   Event loop manages task execution.\
-   Callback hell → deeply nested callbacks.\
-   Inversion of control → losing control when passing callbacks to
    another function.


======================================================================================================================


# JavaScript Promises

## 1. What is a Promise?

A **Promise** in JavaScript is an object that represents the eventual
**completion (or failure)** of an asynchronous operation.\
It acts as a placeholder for a value that will be available **in the
future**.

------------------------------------------------------------------------

## 2. How to Create a New Promise?

A Promise is created using the `Promise` constructor, which takes a
function with two parameters: **resolve** and **reject**.

### Example

``` js
const myPromise = new Promise((resolve, reject) => {
  let success = true;

  if (success) {
    resolve("Promise resolved successfully!");
  } else {
    reject("Promise rejected with an error.");
  }
});
```

------------------------------------------------------------------------

## 3. States of a Promise

A Promise has **3 possible states**:

1.  **Pending** → Initial state, neither fulfilled nor rejected.
2.  **Fulfilled** → Operation completed successfully (`resolve()`
    called).
3.  **Rejected** → Operation failed (`reject()` called).

### Example

``` js
const promise = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Done!"), 1000);
});

console.log(promise); // Initially: pending
// After 1 second: fulfilled with value "Done!"
```

------------------------------------------------------------------------

## 4. How to Consume an Existing Promise?

We use `.then()`, `.catch()`, and `.finally()` to handle promises.

### Example

``` js
const myPromise = new Promise((resolve, reject) => {
  let success = false;

  if (success) {
    resolve("Data fetched successfully");
  } else {
    reject("Failed to fetch data");
  }
});

myPromise
  .then(result => {
    console.log("Fulfilled:", result);
  })
  .catch(error => {
    console.log("Rejected:", error);
  })
  .finally(() => {
    console.log("Always executed");
  });
```

**Output (if success = false):**

    Rejected: Failed to fetch data
    Always executed

------------------------------------------------------------------------

# ✅ Summary

-   A Promise is used to handle async operations.\
-   Created with `new Promise((resolve, reject) => {...})`.\
-   Has 3 states: **pending, fulfilled, rejected**.\
-   Consumed with `.then()`, `.catch()`, `.finally()`.


======================================================================================================================

# JavaScript Promises Guide

This guide contains explanations and examples for various Promise concepts in JavaScript.

---

## 1. Promise Chaining
```js
function task1() {
    return new Promise(resolve => setTimeout(() => resolve('Task 1 complete'), 1000));
}

function task2(message) {
    return new Promise(resolve => setTimeout(() => resolve(message + ' & Task 2 complete'), 1000));
}

task1()
    .then(result => task2(result))
    .then(finalResult => console.log(finalResult));
// Output after 2 seconds: "Task 1 complete & Task 2 complete"
```

---

## 2. Handling errors in a promise chain using `.catch`
```js
function willReject() {
    return new Promise((_, reject) => reject('Something went wrong'));
}

willReject()
    .then(result => console.log(result))
    .catch(error => console.error('Error caught:', error));
// Output: "Error caught: Something went wrong"
```

---

## 3. `.finally` block in a promise chain
```js
Promise.resolve('Done')
    .then(result => console.log(result))
    .finally(() => console.log('Cleanup actions'));
// Output:
// Done
// Cleanup actions
```

---

## 4. Error inside `.then` with `.catch`
```js
Promise.resolve()
    .then(() => { throw new Error('Oops!'); })
    .catch(error => console.error('Caught:', error.message));
// Output: "Caught: Oops!"
```

## 5. Error inside `.then` without `.catch`
```js
Promise.resolve()
    .then(() => { throw new Error('Oops!'); });
// Output: UnhandledPromiseRejectionWarning (depends on environment)
```

## 6. Why `.catch` should be at the end
- `.catch` should be at the **end** to handle any errors thrown anywhere in the chain.

## 7. Consuming multiple promises by chaining
```js
function p1() { return Promise.resolve('P1'); }
function p2() { return Promise.resolve('P2'); }

p1()
    .then(result => { console.log(result); return p2(); })
    .then(result => console.log(result));
// Output: P1
// P2
```

## 8. Consuming multiple promises using `Promise.all`
```js
const promises = [
    Promise.resolve('A'),
    Promise.resolve('B'),
    Promise.resolve('C')
];

Promise.all(promises)
    .then(results => console.log(results));
// Output: ['A','B','C']
```

## 9. Error handling with promises
- Always use `.catch` or `try/catch` with `async/await`.
- Handles network errors, invalid data, etc.

## 10. Why error handling is important
- Without error handling, failed promises can crash apps or lead to inconsistent states.

## 11. Promisifying callback-based functions
```js
function delay(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

delay(1000).then(() => console.log('1 second passed'));
```
- For Node.js fs.readFile:
```js
const fs = require('fs');
const fsPromises = require('fs').promises;

fsPromises.readFile('file.txt', 'utf-8')
    .then(data => console.log(data))
    .catch(err => console.error(err));
```

## 12. `Promise.resolve` and `Promise.reject`
```js
Promise.resolve('Success').then(console.log);
Promise.reject('Failure').catch(console.error);
```

## 13. `Promise.all`
- Resolves when all promises resolve, rejects if any reject.

## 14. `Promise.allSettled`
```js
const promises = [Promise.resolve(1), Promise.reject('err')];
Promise.allSettled(promises)
    .then(results => console.log(results));
// Output: [{status:'fulfilled', value:1}, {status:'rejected', reason:'err'}]
```

## 15. `Promise.any`
```js
const promises = [Promise.reject('X'), Promise.resolve('Y')];
Promise.any(promises).then(console.log); // Output: 'Y'
```
- Resolves with first fulfilled promise, ignores rejections unless all fail.

## 16. `Promise.race`
```js
const p1 = new Promise(res => setTimeout(() => res('First'), 500));
const p2 = new Promise(res => setTimeout(() => res('Second'), 1000));
Promise.race([p1, p2]).then(console.log); // Output: 'First'
```
- Resolves/rejects with the **first promise** that settles.



