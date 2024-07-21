# Promise APIs

Promise APIs in JavaScript provide a set of methods that facilitate working with promises. These methods allow you to handle multiple promises, manage their outcomes, and create promises in a more convenient way. Here are some of the key Promise APIs:

### 1. `Promise.all()`

The `Promise.all()` method takes an iterable (e.g., an array) of promises and returns a single promise that resolves when all the promises in the iterable have resolved or rejects when any promise in the iterable rejects. It is useful for running multiple asynchronous operations in parallel and waiting for all of them to complete.

```javascript
const promise1 = Promise.resolve(3);
const promise2 = 42;
const promise3 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, "foo");
});

Promise.all([promise1, promise2, promise3])
  .then((values) => {
    console.log(values); // [3, 42, "foo"]
  })
  .catch((error) => {
    console.error(error);
  });
```

### 2. `Promise.race()`

The `Promise.race()` method takes an iterable of promises and returns a single promise that resolves or rejects as soon as one of the promises in the iterable resolves or rejects. It is useful for scenarios where you want to proceed as soon as any one of multiple asynchronous operations completes.

```javascript
const promise1 = new Promise((resolve, reject) => {
  setTimeout(resolve, 500, "one");
});
const promise2 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, "two");
});

Promise.race([promise1, promise2])
  .then((value) => {
    console.log(value); // "two"
  })
  .catch((error) => {
    console.error(error);
  });
```

### 3. `Promise.any()`

The `Promise.any()` method takes an iterable of promises and returns a single promise that resolves as soon as any one of the promises in the iterable resolves, or rejects if all of the promises reject. It is useful for scenarios where you want to proceed with the first successful result.

```javascript
const promise1 = new Promise((resolve, reject) => {
  setTimeout(reject, 100, "one");
});
const promise2 = new Promise((resolve) => {
  setTimeout(resolve, 200, "two");
});
const promise3 = new Promise((resolve, reject) => {
  setTimeout(reject, 300, "three");
});

Promise.any([promise1, promise2, promise3])
  .then((value) => {
    console.log(value); // "two"
  })
  .catch((error) => {
    console.error("All promises were rejected");
  });
```

### 4. `Promise.allSettled()`

The `Promise.allSettled()` method takes an iterable of promises and returns a single promise that resolves when all of the promises have either resolved or rejected. It provides an array of objects representing the outcome of each promise.

```javascript
const promise1 = Promise.resolve(3);
const promise2 = new Promise((resolve, reject) => {
  setTimeout(reject, 100, "foo");
});
const promise3 = Promise.resolve(42);

Promise.allSettled([promise1, promise2, promise3]).then((results) => {
  results.forEach((result) => {
    if (result.status === "fulfilled") {
      console.log("Fulfilled:", result.value);
    } else {
      console.log("Rejected:", result.reason);
    }
  });
});
```

### 5. `Promise.resolve()`

The `Promise.resolve()` method returns a Promise object that is resolved with a given value. If the value is a promise, it will be returned as is.

```javascript
Promise.resolve("Success").then((value) => {
  console.log(value); // "Success"
});
```

### 6. `Promise.reject()`

The `Promise.reject()` method returns a Promise object that is rejected with a given reason.

```javascript
Promise.reject(new Error("Failure")).catch((error) => {
  console.error(error); // Error: Failure
});
```

### Summary

These Promise APIs provide powerful tools for working with asynchronous operations in JavaScript, allowing you to manage multiple promises, handle their outcomes, and create promises conveniently. They are essential for writing clean, readable, and maintainable asynchronous code.
