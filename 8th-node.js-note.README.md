# Namaste Node.js — Episode 8: V8 JavaScript Engine

## Overview

This episode dives into **Google's V8 JavaScript engine** and explains how JavaScript goes from source code to execution, including parsing, AST, bytecode, JIT compilation, optimization, and garbage collection.

## 1. What is V8?

**V8** is Google's JavaScript engine used by Node.js to execute JavaScript.

```text
Node.js
  ↓
V8 → Executes JavaScript
```

> V8 is the JavaScript engine inside Node.js that executes my JavaScript.

## 2. Parsing

When JavaScript is given to V8:

```text
Source Code
    ↓
Tokenization
    ↓
AST
```

* **Tokenization** → breaks code into meaningful tokens.
* **AST (Abstract Syntax Tree)** → represents the structure of the code.

Example:

```js
var a = 10;
```

Tokens include `var`, `a`, `=`, and `10`.

A syntax error occurs when V8 cannot correctly understand the structure of the code.

## 3. Interpreter vs Compiler

**Interpreter:** Executes code step by step.

**Compiler:** Converts code into machine code before execution.

V8 uses **both**, which is called **Just-In-Time (JIT) compilation**.

## 4. Ignition

**Ignition** is V8's interpreter.

```text
AST
 ↓
Ignition
 ↓
Bytecode
 ↓
Execution
```

Bytecode is a lower-level representation of JavaScript that V8 can execute.

## 5. TurboFan & Hot Code

V8 looks for code that executes frequently. This is called **hot code**.

```text
Code runs repeatedly
        ↓
     Hot Code
        ↓
     TurboFan
        ↓
Optimized Machine Code
        ↓
   Faster execution
```

**TurboFan** is V8's optimizing compiler.

## 6. De-optimization

V8 may optimize code based on assumptions.

Example:

```js
function sum(a, b) {
    return a + b;
}
```

If it repeatedly receives numbers, V8 may optimize it for numbers.

If it later receives unexpected types, those assumptions may become invalid, causing **de-optimization**.

```text
Optimization
     ↓
Assumption becomes invalid
     ↓
De-optimization
     ↓
Interpreter path
```

Consistent input types can help V8 make useful optimization assumptions.

## 7. Complete V8 Flow

```text
JavaScript
    ↓
Parsing
    ↓
Tokens
    ↓
AST
    ↓
Ignition
    ↓
Bytecode
    ↓
Execution
    ↓
Hot Code
    ↓
TurboFan
    ↓
Optimized Machine Code
    ↓
Faster Execution
    ↓
Possible De-optimization
```

This is the main flow to remember.

## 8. Garbage Collection

V8 also manages memory using **Garbage Collection**.

Its purpose is to free memory that the program no longer needs.

**Mark-and-Sweep** identifies memory that is still needed and cleans up unused memory.

You don't need to memorize every collector name such as Orinoco, Oilpan, or Scavenger.

## Interview Quick Revision

**What is V8?**
Google's JavaScript engine used by Node.js.

**What is an AST?**
A tree representation of JavaScript code structure.

**What is tokenization?**
Breaking source code into meaningful tokens.

**What is Ignition?**
V8's interpreter that converts AST into bytecode.

**What is bytecode?**
A lower-level form of code that V8 can execute.

**What is TurboFan?**
V8's optimizing compiler.

**What is hot code?**
Code that executes frequently and may be optimized.

**What is JIT?**
Just-In-Time compilation — V8 uses interpretation and compilation while the program runs.

**What is de-optimization?**
Removing/reversing an optimization when its assumptions become invalid.

**Why keep input types consistent?**
Consistent types can help V8 optimize code effectively.

**What is garbage collection?**
Automatically freeing memory that is no longer needed.

**Are Ignition and TurboFan used by every JS engine?**
No. They are V8-specific names.

## Final Mental Model

```text
Source Code
    ↓
Parsing → Tokens → AST
    ↓
Ignition → Bytecode
    ↓
Execution
    ↓
Hot Code
    ↓
TurboFan → Optimization
    ↓
Faster Execution
    ↓
If assumptions fail → De-optimization

V8 also performs
Garbage Collection → Frees unused memory
```

> **Don't memorize V8's source code. Understand the flow: Source → AST → Ignition → Bytecode → Execution → Hot Code → TurboFan → Optimization → Possible De-optimization.**
