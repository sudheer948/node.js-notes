# Namaste Node.js — Season 1, Episode 6

## Core Idea

Node.js uses the **V8 JavaScript engine** and **libuv** to provide asynchronous I/O.

JavaScript execution itself is **synchronous and single-threaded**, but Node.js can handle slow I/O without making the main JavaScript thread wait.

---

## 1. JavaScript: Synchronous & Single-Threaded

**Synchronous** means JavaScript executes code one step at a time.

**Single-threaded** means JavaScript execution happens on one main thread.

> JavaScript runs one piece of code at a time on the main thread.

---

## 2. Synchronous vs Asynchronous

### Synchronous

The next task waits until the current task finishes.

### Asynchronous

A slow task can start while JavaScript continues doing other work. When the task finishes, its callback can run.

### Restaurant Example

- **Synchronous:** The next customer waits until the current order is finished.
- **Asynchronous:** A slow order goes to a waiting area while other customers are served.

---

## 3. Blocking vs Non-Blocking

**Blocking:** The main JavaScript thread has to wait for an operation to finish.

**Non-blocking:** The main JavaScript thread can continue doing other work.

> Blocking makes the main thread wait. Non-blocking lets it continue.

---

## 4. V8

**V8** is the JavaScript engine used by Node.js.

It provides:

- JavaScript execution
- Call Stack
- Memory Heap
- Garbage Collection

### Call Stack

The Call Stack keeps track of the JavaScript code currently being executed.

When a function is called, a **Function Execution Context** is created and placed on the Call Stack. When the function finishes, it is removed.

### Memory Heap

The Memory Heap stores data used by the program.

### Garbage Collector

The Garbage Collector removes memory that is no longer needed.

---

## 5. Why Node.js Needs More Than V8

V8 executes JavaScript, but it does not directly provide capabilities such as:

- File access
- Timers
- Network operations

Node.js provides these extra runtime capabilities around V8.

---

## 6. libuv

**libuv** is a key library used by Node.js for asynchronous operations.

It acts as an important layer between Node.js/V8 and the operating system.

### Basic Flow

```text
JavaScript
    ↓
V8
    ↓
Async Task
    ↓
libuv
    ↓
Operating System / Async Handling
    ↓
Callback
    ↓
V8