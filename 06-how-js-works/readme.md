# How JavaScript Works

### Core Fundamental

Everything in JavaScript happens inside the **execution context**. You can assume this execution context to be a big box or a container in which the whole JavaScript code is executed.

### Execution Context

Let us now see how this execution context actually looks like. Follow along with me.

#### Components of Execution Context

Execution context is like a big box and it has two components in it:

1. **Memory Component**:

   - This is the place where all the variables and functions are stored as key-value pairs, something like this:
     ```
     key: value
     ```
     If we have a variable `a` which is equal to `10`, it will be stored here. Similarly, functions are also stored in this memory component.
   - There is also a heavy word for this memory component, and this memory component is also known as **variable environment**.

2. **Code Component**:
   - This is the place where code is executed one line at a time.
   - Just like the memory component is also known as the variable environment, the code component is also known as **thread of execution**.
   - This thread of execution is like a thread in which the whole code is executed one line at a time.

### JavaScript: Synchronous and Single-Threaded

Here's another core fundamental. Listen carefully:

JavaScript is a **synchronous, single-threaded** language.

#### What Does This Mean?

- **Single-Threaded**: JavaScript can only execute one command at a time.
- **Synchronous**: JavaScript can only execute one command at a time and in a specific order. It can only go to the next line once the current line has finished executing.

Let's revise: JavaScript is a synchronous, single-threaded language.

### Asynchronous JavaScript

You might be thinking, "We have heard of something known as AJAX where 'A' stands for asynchronous. What does that mean?"

Don't worry, we'll cover everything. We'll be going slowly and understanding each of these concepts properly as we go ahead. For now, just remember that JavaScript is not possible without this beautiful execution context.

### Recap

- **Execution Context**: The whole thing where JavaScript code is executed.
  - **Memory Component (Variable Environment)**: Contains variables and functions as key-value pairs.
  - **Code Component (Thread of Execution)**: The place where the whole JavaScript code is executed.
