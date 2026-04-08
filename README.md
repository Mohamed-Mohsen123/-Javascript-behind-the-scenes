# JavaScript Behind the Scenes

---

![JavaScript Engine](/assests/img/Screenshot%202026-04-08%20174446.png)

## 1-JavaScript Engine - Simplified Explanation

### 1) Parser

- Converts the code into small parts (Tokens).
- Identifies the keywords.
- Also detects if there are any errors in the code.

---

### 2) Abstract Syntax Tree (AST)

- A type of data structure.
- Responsible for converting the code into a tree structure (Tree).
- This tree illustrates the structure of the code and the relationships between its parts.

---

### 3) Compilers in the JavaScript Engine

#### 1) Interpreter

- Executes the code line by line.
- Simultaneously translates it into machine language for the device to understand.
- Advantage: Starts execution quickly.
- Disadvantage: Performance can be lower in some cases.

#### 2) Compiler

- Translates the entire code into machine language at once.
- Then starts execution.
- Advantage: Higher performance.
- Disadvantage: Takes time before starting execution.

---

### Solution: JIT Compiler (Just-In-Time)

- Instead of using the Interpreter or Compiler alone, both are combined.
- Execution starts using the Interpreter.
- Then performance is optimized using the Compiler for the important parts of the code.

---

## Summary

- **Parser**: Code analysis
- **AST**: Converting code into a tree
- **Interpreter and Compiler**: Code execution
- **JIT**: Combining the advantages of both

---

## 2-Call Stack & Memory Heap in JavaScript

#### 1)The Memory Heap is where JavaScript stores:

Objects { }
Arrays [ ]
Functions
Complex data

#### 2)The Call Stack is a stack (LIFO):

Last In → First Out
It tracks function calls
Example:

```javascript
function one() {
  two();
}

function two() {
  console.log("Hello");
}

one();
```

Execution flow:

- `one()` pushed to stack
- Inside it → `two()` pushed
- `console.log()` runs
- `two()` removed
- `one()` removed

---

## 3-Javascript Garbage Collection & Memory Leaks

---

### JavaScript Garbage Collection

JavaScript handles memory automatically — you don’t manually free memory like in C/C++.

The engine (like V8 in Chrome) uses Garbage Collection to remove unused memory.

Core Idea: Reachability

An object is kept in memory if it’s reachable, meaning:

It’s referenced by a variable
It’s part of a chain of references from global scope

If it’s not reachable → it gets deleted

### Memory Leaks in JavaScript

Memory is no longer needed but still not garbage collected

#### Common Causes of Memory Leaks:

1. Global Variables

```javascript
function leak() {
  name = "Mohamed"; // forgot let/const → becomes global
}
```

✔ Fix:

```javascript
let name = "Mohamed";
```

2. setInterval / setTimeout

```javascript
setInterval(() => {
  console.log("Running...");
}, 1000);
```

👉 If not cleared → keeps running forever

✔ Fix:

```javascript
const id = setInterval(() => {}, 1000);
clearInterval(id);
```

3. Event Listeners Not Removed

```javascript
button.addEventListener("click", handler);
```

👉 If element removed but listener not → memory leak

✔ Fix:

```javascript
button.removeEventListener("click", handler);
```

## 4-JavaScript Single Thread & Runtime

JavaScript executes one task at a time.

It uses one Call Stack and runs code synchronously by default.

JavaScript runs inside environments like:

Browser
Node.js

These provide features to handle asynchronous operations

### Runtime Components

1.  Call Stack
    Executes functions
    Works as LIFO (Last In → First Out)

2.  Web APIs
    Handle async operations outside the Call Stack

         Examples:

         setTimeout
         setInterval
         fetch
         DOM events

3.  Callback Queue
    Stores callbacks from async tasks
    Waits until Call Stack is empty

4.  Event Loop
    Monitors Call Stack & Callback Queue

👉 Rule:

If Call Stack is empty → move callback to stack
Otherwise → wait
