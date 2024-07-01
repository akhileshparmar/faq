# How JS code is executed

To understand how JavaScript code execution and memory allocation work together, it’s important to break down the process into distinct phases: **memory allocation** and **code execution**. Here’s a step-by-step explanation of how these processes interact:

### 1. Memory Allocation

Memory allocation in JavaScript involves reserving space for variables, objects, functions, and other data structures during code execution. This process can be divided into two primary areas: the **stack** and the **heap**.

#### **a. Stack Allocation**

The stack is used for managing function calls and local variables:

- **Function Calls**: When a function is invoked, a new stack frame is created for it. This frame includes local variables, parameters, and information about the function’s execution context.
- **Execution Context**: Each function call creates a new execution context, which is pushed onto the stack. The context includes variables, the `this` value, and the scope chain.

#### **b. Heap Allocation**

The heap is used for dynamic memory allocation of objects and arrays:

- **Objects and Arrays**: These data structures do not have a fixed size and are allocated on the heap. Memory is reserved for them at runtime, and they can grow or shrink in size.
- **Garbage Collection**: The JavaScript engine automatically manages heap memory. The garbage collector identifies objects that are no longer reachable and reclaims their memory.

### 2. Code Execution

Once memory is allocated, the JavaScript engine executes the code. This involves parsing, compiling, and running the code while managing the stack and heap.

#### **a. Parsing and Compilation**

1. **Parsing**:

   - The JavaScript engine parses the source code into an Abstract Syntax Tree (AST). This step involves tokenizing the code and checking for syntax errors.

2. **Compilation**:
   - The AST is converted into bytecode or machine code. Modern engines use Just-In-Time (JIT) compilation to optimize the code during execution.

#### **b. Execution**

1. **Call Stack**:

   - **Function Calls**: When a function is called, a new execution context is created and pushed onto the call stack. The function’s code is executed within this context.
   - **Local Variables**: Variables declared within the function are allocated on the stack frame for that function call.
   - **Return**: Once the function completes execution, its stack frame is popped off the stack, and control returns to the calling context.

2. **Event Loop**:
   - **Task Queue**: Handles callbacks from asynchronous operations (e.g., `setTimeout`). Once the call stack is empty, tasks from the task queue are processed.
   - **Microtask Queue**: Handles promise callbacks and other microtasks. Microtasks are processed after the current script has finished and before tasks from the task queue.

### Summary

- **Memory Allocation**: Involves the stack for function calls and local variables, and the heap for dynamic objects and arrays. The stack is used for quick allocation and deallocation, while the heap is managed by the garbage collector.
- **Code Execution**: The JavaScript engine parses and compiles code into an executable format. The call stack manages function calls and execution contexts, while the event loop coordinates the execution of asynchronous tasks and microtasks.

This process ensures that JavaScript can efficiently handle both synchronous and asynchronous operations while managing memory effectively.
