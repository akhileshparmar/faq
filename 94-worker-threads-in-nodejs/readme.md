# Worker threads in Node.js

Worker threads in Node.js allow you to run JavaScript code in parallel using multiple threads. This is particularly useful for CPU-intensive operations, as it helps to offload heavy computations from the main thread, keeping your application responsive.

### Key Concepts of Worker Threads

1. **Main Thread**: The primary thread where your Node.js application runs.
2. **Worker Thread**: Additional threads that can execute code in parallel with the main thread.
3. **Worker Pool**: A set of worker threads managed by the main thread.

### Creating and Using Worker Threads

To use worker threads, you'll need to import the `worker_threads` module. Here's a step-by-step example of creating and using worker threads in Node.js:

#### Step 1: Install Node.js (if not already installed)

Ensure you have Node.js installed. You can download it from the [official website](https://nodejs.org/).

#### Step 2: Create a Worker Thread

Create a file named `worker.js` which will contain the code to be executed by the worker thread.

```javascript
// worker.js
const { parentPort } = require("worker_threads");

const compute = () => {
  let sum = 0;
  for (let i = 0; i < 1e9; i++) {
    sum += i;
  }
  return sum;
};

// Send the result back to the main thread
parentPort.postMessage(compute());
```

#### Step 3: Create the Main Script

Create another file named `main.js` which will create and manage the worker threads.

```javascript
// main.js
const { Worker } = require("worker_threads");

console.log("Main thread starting...");

const createWorker = (filePath) => {
  return new Promise((resolve, reject) => {
    const worker = new Worker(filePath);

    worker.on("message", (result) => {
      console.log(`Worker result: ${result}`);
      resolve(result);
    });

    worker.on("error", (error) => {
      console.error(`Worker error: ${error}`);
      reject(error);
    });

    worker.on("exit", (code) => {
      if (code !== 0) {
        console.error(`Worker stopped with exit code ${code}`);
      }
    });
  });
};

(async () => {
  try {
    const result1 = await createWorker("./worker.js");
    const result2 = await createWorker("./worker.js");
    console.log(`Results: ${result1}, ${result2}`);
  } catch (error) {
    console.error(error);
  }
})();

console.log("Main thread ending...");
```

### Explanation

- **worker.js**:

  - Defines a `compute` function to perform a heavy computation.
  - Uses `parentPort.postMessage` to send the result back to the main thread.

- **main.js**:
  - Imports the `Worker` class from `worker_threads`.
  - Defines a `createWorker` function to create and manage worker threads.
  - Uses `Promise` to handle asynchronous worker operations.
  - Creates and starts two workers, each running `worker.js`.
  - Logs results received from the workers.

### Running the Example

1. Open a terminal.
2. Navigate to the directory containing `worker.js` and `main.js`.
3. Run the main script using Node.js:
   ```bash
   node main.js
   ```

You should see output indicating that the main thread is running, worker threads are processing, and results are received from the workers.

### Use Cases for Worker Threads

- **CPU-Intensive Tasks**: Such as complex calculations, data processing, image manipulation, and other heavy computations.
- **Isolated Tasks**: Running tasks that should not interfere with the main thread's event loop, ensuring your application remains responsive.

By using worker threads, you can significantly improve the performance of CPU-bound tasks in your Node.js applications, while maintaining the responsiveness of the main event loop for handling I/O-bound tasks.
