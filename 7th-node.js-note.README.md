# Namaste Node.js — Episode 7

## Synchronous vs Asynchronous JavaScript

This episode covers V8, libuv, the Call Stack, callbacks, blocking code, CommonJS `require()`, core modules, `pbkdf2()`, and timers.

## 1. Synchronous vs Asynchronous

**Synchronous:** JavaScript waits for the current operation to finish.

**Asynchronous:** An operation can start while JavaScript continues executing other work.

```text
Synchronous → V8 → Execute
Async → Node.js/libuv → Continue → Callback later
```

> V8 executes JavaScript, while Node.js uses mechanisms such as libuv for asynchronous work.

## 2. Call Stack

JavaScript executes through the **Call Stack**.

```text
Function called → Push to Stack
Function finishes → Remove from Stack
```

An asynchronous callback cannot interrupt currently running JavaScript. It waits until the Call Stack becomes available.

## 3. CommonJS `require()`

`require()` is **synchronous** in CommonJS.

```js
const fs = require("fs");
const crypto = require("crypto");
```

The module loads before execution continues.

## 4. Node.js Core Modules

| Module    | Purpose               |
| --------- | --------------------- |
| `fs`      | File system           |
| `https`   | Networking            |
| `crypto`  | Cryptography          |
| `os`      | OS information        |
| `zlib`    | Compression           |
| `console` | Console functionality |

The `node:` prefix explicitly identifies a built-in module:

```js
require("node:fs");
require("node:crypto");
```

## 5. Async Operations

```text
Async starts
    ↓
Node.js/libuv handles work
    ↓
V8 continues JavaScript
    ↓
Operation finishes
    ↓
Callback waits
    ↓
Call Stack free → Callback runs
```

Async operations can finish in a different order from how they started.

## 6. `pbkdf2()` vs `pbkdf2Sync()`

**`pbkdf2()`**

* Asynchronous
* Main thread can continue
* Uses callback

**`pbkdf2Sync()`**

* Synchronous
* Main thread waits
* Can block JavaScript

```text
pbkdf2()     → Async → Continue
pbkdf2Sync() → Sync  → Block
```

CPU-heavy synchronous work can delay requests, callbacks, and other JavaScript.

## 7. `setTimeout()`

```js
setTimeout(() => {
    console.log("Timer");
}, 1000);
```

The delay is a **minimum delay**, not a guaranteed execution time.

### `setTimeout(0)`

```js
console.log("Hello");

setTimeout(() => console.log("Timer"), 0);

console.log("End");
```

Output:

```text
Hello
End
Timer
```

`setTimeout(0)` does **not** mean immediate. The current JavaScript must finish first.

## 8. Node.js Source Code

Node.js is built from real source code. APIs such as `require()` and core modules can be explored in the Node.js repository.

The goal isn't to memorize the source code, but to understand how Node.js works internally.

## Interview Quick Revision

**Synchronous vs Async:** Sync waits; async allows JavaScript to continue.

**Why is `require()` synchronous?**
CommonJS loads the module before execution continues.

**What is blocking?**
The main JavaScript thread is busy and cannot execute other JavaScript.

**Does `setTimeout(0)` run immediately?**
No. It waits for the current JavaScript execution to finish.

**Does `setTimeout(1000)` guarantee exactly 1 second?**
No. It only provides a minimum delay.

**Why is `pbkdf2Sync()` dangerous on a server?**
It can block the main JavaScript thread.

**Why can async callbacks execute in different orders?**
Because operations can take different amounts of time.

## Final Mental Model

```text
V8
 ↓
Executes JavaScript

Async Work
 ↓
Node.js / libuv
 ↓
JavaScript continues
 ↓
Callback waits
 ↓
Call Stack available
 ↓
Callback executes

Sync CPU-heavy work
 ↓
Blocks main thread
 ↓
Everything else waits
```

> **Synchronous work blocks. Asynchronous work allows JavaScript to continue. Callbacks run when the Call Stack is available.**
