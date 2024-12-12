# Fork Method in Node.js

The `fork()` method in Node.js is part of the **Child Processes** module. It is used to create a new child process that runs a separate instance of a JavaScript file. This method is designed to make it easy to spawn child processes that can communicate with the parent process using **inter-process communication (IPC)**.

---

### **How the `fork()` Method Works**

- It is a specialized version of `spawn()`.
- The child process runs a specific JavaScript file in a new Node.js instance.
- The parent and child processes can communicate via a built-in messaging system.

---

### **Syntax**

```javascript
const { fork } = require("child_process");

const child = fork("path/to/script.js", [args], options);
```

---

### **Parameters**

1. **`script`**: Path to the JavaScript file to execute in the child process.
2. **`args`** (optional): Array of command-line arguments passed to the child process.
3. **`options`** (optional): Configuration object, such as:
   - `cwd`: Current working directory for the child process.
   - `env`: Environment variables for the child process.
   - `silent`: If `true`, pipes the child process’s `stdout` and `stderr` to the parent process.

---

### **Features**

- Uses a new Node.js instance in the child process.
- Enables bi-directional communication between parent and child via the `.send()` and `.on('message')` methods.

---

### **Example: Parent and Child Communication**

#### Parent Process:

```javascript
const { fork } = require("child_process");

const child = fork("./child.js");

// Send a message to the child process
child.send({ greeting: "Hello Child" });

// Listen for messages from the child
child.on("message", (message) => {
  console.log("Message from child:", message);
});
```

#### Child Process (`child.js`):

```javascript
process.on("message", (message) => {
  console.log("Message from parent:", message);

  // Send a response back to the parent
  process.send({ reply: "Hello Parent" });
});
```

---

### **When to Use `fork()`**

1. To perform **CPU-intensive tasks** in a separate process, avoiding blocking the event loop.
2. When you need **communication** between parent and child processes.
3. For **scaling applications**, such as creating worker processes in a cluster.

---

### **Key Points**

- Processes created with `fork()` are isolated; they do not share memory with the parent.
- Use it for **multi-process applications** in scenarios requiring efficient IPC.
- For heavy computation or independent tasks, consider alternatives like `worker_threads` if shared memory is needed.
