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
