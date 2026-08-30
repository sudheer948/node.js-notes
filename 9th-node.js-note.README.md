# Namaste Node.js — Episode 9: Event Loop

## Overview

This episode explains **libuv, the Event Loop, its phases, callback queues, `process.nextTick()`, Promises, and how to reason about async output order**.

## 1. One Mental Model

```text
V8 → Runs JavaScript
libuv → Helps handle async work
Event Loop → Sends ready callbacks to Call Stack
```

> **V8 runs JavaScript. Libuv helps with async work. The Event Loop decides when ready callbacks can run.**

## 2. Basic Async Flow

```text
Async operation starts
        ↓
Node.js / libuv handles it
        ↓
JavaScript continues
        ↓
Operation finishes
        ↓
Callback becomes ready
        ↓
Event Loop checks
        ↓
Callback → Call Stack
        ↓
V8 executes callback
```

## 3. Event Loop Phases

The four main phases are:

```text
Timer → Poll → Check → Close
```

| Phase     | Handles                         |
| --------- | ------------------------------- |
| **Timer** | `setTimeout()`, `setInterval()` |
| **Poll**  | Mainly I/O callbacks            |
| **Check** | `setImmediate()`                |
| **Close** | Close/cleanup callbacks         |

## 4. Timer Phase

`setTimeout()` and `setInterval()` callbacks are handled in the Timer phase.

A timer delay is a **minimum delay**, not an exact execution time.

```text
setTimeout(1000)
      ↓
Minimum 1 second
      ↓
Callback runs when eligible
```

## 5. `process.nextTick()` & Promises

In this episode's model:

```text
process.nextTick()
       ↓
Promise callback
       ↓
Next Event Loop phase
```

`process.nextTick()` uses Node.js's high-priority nextTick queue.

A `nextTick()` callback can schedule another `nextTick()`, which runs before later phases.

## 6. Async Output Order

Don't assume callbacks execute in the order operations started.

```text
Operation A starts
Operation B starts
Operation C starts

Completion may be:
B → C → A
```

Different async operations take different amounts of time, so callbacks run when their work is ready.

## 7. `setTimeout()` vs `setImmediate()`

Don't memorize:

> "`setTimeout()` always runs first."

or:

> "`setImmediate()` always runs first."

The order depends on **where they are scheduled and the current Event Loop phase**.

Inside an I/O callback, `setImmediate()` can run before a newly scheduled timer because execution can move from **Poll → Check → Timer**.

## 8. Event Loop Doesn't Restart

The Event Loop doesn't restart from Timer after every callback.

It continues from its **current position in the cycle**.

```text
Current phase
     ↓
Next phase
     ↓
Next phase...
```

## 9. Poll Can Wait

If there is no immediate work but I/O may become ready, the Event Loop can wait in the Poll phase.

```text
No immediate work
      ↓
I/O may become ready
      ↓
Wait at Poll
      ↓
I/O ready → Callback runs
```

## Interview Quick Revision

**What is the Event Loop?**
It checks for ready callbacks and sends them to the Call Stack when JavaScript is free.

**What are the four phases?**
Timer → Poll → Check → Close.

**Timer phase?**
`setTimeout()` / `setInterval()`.

**Poll phase?**
Mainly I/O callbacks.

**Check phase?**
`setImmediate()` callbacks.

**Close phase?**
Close and cleanup callbacks.

**What is `process.nextTick()`?**
A high-priority Node.js callback queue.

**Which runs first: `nextTick()` or Promise?**
`process.nextTick()` in this episode's examples.

**Does `setTimeout(0)` mean immediate?**
No. It still waits until it is eligible and the Timer phase can run it.

**Does `setImmediate()` always beat `setTimeout()`?**
No. It depends on context.

**Why can callbacks finish in different orders?**
Async operations take different amounts of time.

## Output Question Strategy

```text
1. Handle synchronous code
2. Check process.nextTick()
3. Check Promise callbacks
4. Identify timers, I/O and setImmediate
5. Find the current Event Loop phase
6. Follow the phase order
```

## Final Mental Model

```text
V8 → Runs JavaScript
        ↓
Async work → libuv
        ↓
Callback becomes ready
        ↓
Event Loop
Timer → Poll → Check → Close
        ↓
Callback → Call Stack
        ↓
V8 executes it

Priority:
nextTick → Promise → Event Loop phases
```

> **Don't memorize output orders. Understand the phase, callback type, and when the async operation becomes ready.**
