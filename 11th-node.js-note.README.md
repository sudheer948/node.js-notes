# Namaste Node.js — Episode 11: Event Loop in Practice

## Overview

Covers **Event Loop, callbacks, timers, Promises, `process.nextTick()`, `setImmediate()`, I/O, execution order, and interview traps.**

## 1. Big Picture

```text
V8 → Executes JavaScript
Node.js/libuv → Handles async work
Event Loop → Coordinates ready callbacks
```

The Event Loop does **not** make JavaScript execute in parallel. JavaScript callbacks still execute one at a time on the main thread.

## 2. Synchronous Code First

The current Call Stack must finish before asynchronous callbacks run.

> **Async callbacks cannot interrupt currently executing synchronous JavaScript.**

## 3. `nextTick()` & Promises

After synchronous code, the practical order is:

```text
Synchronous
    ↓
process.nextTick()
    ↓
Promise microtasks (.then/.catch/.finally)
    ↓
Event Loop phases
```

`process.nextTick()` has higher priority than Promise microtasks.

Repeatedly scheduling `nextTick()` can cause **Event Loop starvation**, delaying other work.

## 4. `setTimeout()`

```js
setTimeout(callback, delay);
```

The delay is a **minimum threshold**, not an exact execution time.

`setTimeout(fn, 0)` does **not** mean immediate execution.

## 5. `setImmediate()`

`setImmediate()` runs during the **Check phase**.

Don't memorize that it always runs before/after `setTimeout(0)`.

> **Their order depends on the context and current Event Loop state.**

## 6. I/O Callbacks

Async file-system and network operations complete outside the immediate synchronous flow.

```text
I/O starts
   ↓
Operation completes
   ↓
Callback becomes ready
   ↓
Event Loop processes it
```

Independent I/O operations can finish in different orders.

## 7. Event Loop Phases

```text
Timers
  ↓
Pending Callbacks
  ↓
Idle / Prepare
  ↓
Poll
  ↓
Check
  ↓
Close
  ↓
Repeat
```

| Phase            | Remember                        |
| ---------------- | ------------------------------- |
| **Timers**       | `setTimeout()`, `setInterval()` |
| **Pending**      | Deferred I/O callbacks          |
| **Idle/Prepare** | Internal libuv work             |
| **Poll**         | I/O callbacks / waiting for I/O |
| **Check**        | `setImmediate()`                |
| **Close**        | Close/cleanup callbacks         |

One Event Loop iteration is called a **tick**.

## 8. Solving Output Questions

Use this order:

1. Execute synchronous code.
2. Identify `process.nextTick()`.
3. Identify Promise microtasks.
4. Identify timers, I/O, and `setImmediate()`.
5. Process microtasks before normal phase callbacks.
6. For real I/O/timing, don't assume a fixed completion order.

### Example

```js
console.log('A');

setTimeout(() => console.log('B'), 0);

Promise.resolve().then(() => console.log('C'));

process.nextTick(() => console.log('D'));

console.log('E');
```

Output:

```text
A → E → D → C → B
```

## 9. Blocking Code

Long CPU-heavy JavaScript or blocking I/O occupies the main JavaScript thread.

```text
Blocking work
     ↓
Main thread busy
     ↓
Other callbacks wait
     ↓
Requests may be delayed
```

Node.js is excellent for many I/O-bound workloads, but CPU-heavy JavaScript still blocks the main thread unless moved to an appropriate worker mechanism.

## 10. Common Interview Traps

❌ "`setTimeout(0)` runs immediately."
✅ It has a minimum delay/threshold.

❌ "Async means parallel JavaScript."
✅ JavaScript callbacks still execute one at a time.

❌ "Node.js has only one thread."
✅ JavaScript runs on the main thread, while Node.js/libuv can use other threads for certain work.

❌ "All callbacks have the same priority."
✅ `nextTick` and Promise microtasks are processed before normal phase callbacks.

❌ "`setImmediate()` always beats `setTimeout()`."
✅ Their order depends on context.

## Interview Quick Revision

**Event Loop?**
Coordinates asynchronous callbacks while JavaScript runs on the main thread.

**Can async callbacks interrupt synchronous code?**
No. The current Call Stack must finish.

**`nextTick()` vs Promise?**
`nextTick()` is processed first.

**`setTimeout(0)` immediate?**
No.

**Where does `setImmediate()` run?**
Check phase.

**What is starvation?**
High-priority work repeatedly prevents other Event Loop work from getting a chance to run.

**Why is blocking code bad?**
It occupies the main JavaScript thread and delays other callbacks/requests.

## One-Minute Interview Explanation

> **Node.js executes JavaScript on a main thread and uses the Event Loop to coordinate asynchronous callbacks. Synchronous code finishes first, followed by high-priority `nextTick` and Promise microtasks, then Event Loop phases such as Timers, Poll, and Check. `setTimeout()` uses the Timers phase, while `setImmediate()` uses Check, so their order depends on context. Long blocking work should be avoided because it prevents other callbacks from running.**
