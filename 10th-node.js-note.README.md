# Namaste Node.js — Episode 10: Thread Pool & Node.js Internals

## Overview

This episode covers the **libuv Thread Pool, Event Loop internals, OS-level I/O, ePoll, and why Node.js is both single-threaded and multi-threaded**.

## 1. Thread Pool

Node.js runs JavaScript on a **main thread**, but libuv can use worker threads for certain expensive or blocking operations.

```text
JavaScript
    ↓
Main Thread
    ↓
libuv
    ↓
Worker Thread (when required)
```

Examples discussed:

* `fs` operations
* `dns.lookup()`
* `crypto.pbkdf2()`

## 2. Event Loop Phases

The simplified Event Loop model:

```text
Timer → Pending Callbacks → Idle/Prepare
→ Poll → Check → Close → Repeat
```

* **Timer** → `setTimeout()`, `setInterval()`
* **Pending callbacks** → deferred I/O callbacks
* **Idle/Prepare** → internal preparation
* **Poll** → important I/O phase
* **Check** → `setImmediate()`
* **Close** → close/cleanup callbacks

One complete Event Loop cycle is called a **tick**.

## 3. Poll Phase

**Poll** is especially important because it handles most I/O-related activity.

libuv can also wait in Poll when there is no immediate work, instead of constantly using CPU.

```text
No immediate work
      ↓
Wait in Poll
      ↓
I/O / timer becomes ready
      ↓
Continue Event Loop
```

## 4. `uv_run()`

The Event Loop is not just a diagram. libuv implements it in C, with `uv_run()` repeatedly processing the Event Loop.

```text
uv_run()
 ↓
Timers
 ↓
Pending callbacks
 ↓
Idle/Prepare
 ↓
Poll
 ↓
Check
 ↓
Close
 ↓
Repeat
```

## 5. How Thread Pool Works

```text
JavaScript starts operation
        ↓
      libuv
        ↓
Available worker thread
        ↓
Worker performs operation
        ↓
Worker becomes free
        ↓
Result → Callback → V8
```

The default thread-pool size discussed is **4**.

If 5 operations need the pool:

```text
4 → Run
1 → Wait
```

When a worker finishes, the waiting operation gets a thread.

## 6. `UV_THREADPOOL_SIZE`

The thread-pool size can be changed using:

```js
process.env.UV_THREADPOOL_SIZE = 2;
```

With a pool size of 2, roughly two thread-pool operations can run at once.

More threads are **not always better**; the size should match the workload and system resources.

## 7. Single-Threaded or Multi-Threaded?

The best answer is:

> **Node.js executes JavaScript on one main thread, but libuv can use multiple worker threads for certain operations.**

So:

```text
JavaScript execution → Single-threaded
libuv operations     → Can use multiple threads
```

Simply saying "Node.js is single-threaded" is incomplete.

## 8. Network I/O & ePoll

Node.js does **not** create one thread for every incoming connection.

For network I/O:

```text
Client
  ↓
Socket / File Descriptor
  ↓
ePoll (Linux)
  ↓
libuv
  ↓
Event Loop
  ↓
Callback
  ↓
V8
```

**ePoll** allows the OS to monitor many sockets and notify libuv when activity occurs.

`kqueue` is a similar mechanism mentioned for macOS/BSD.

## 9. ePoll vs Thread Pool

Don't confuse them:

| ePoll                    | Thread Pool                              |
| ------------------------ | ---------------------------------------- |
| Monitors I/O connections | Provides worker threads                  |
| OS-level mechanism       | libuv worker mechanism                   |
| Used for network I/O     | Used for certain blocking/expensive work |

## 10. Data Structures

The episode connects Node.js internals with data structures:

* **Timer queue → Min-heap**
* **ePoll → Red-black tree** (as discussed in the episode)

These structures help Node.js efficiently manage timers and I/O-related work.

## 11. `process.nextTick()` vs `setImmediate()`

Don't judge their behavior from their names.

* `process.nextTick()` → high priority
* `setImmediate()` → Check phase

```text
process.nextTick()
      ↓
Higher priority

setImmediate()
      ↓
Check phase
```

## 12. Most Important Lesson: Don't Block

Avoid blocking the main JavaScript thread with:

* Heavy calculations
* Huge/infinite loops
* Unnecessary synchronous methods
* Very heavy `JSON.parse()` / `JSON.stringify()`
* Complex long-running regular expressions

If the Call Stack stays busy, other callbacks must wait.

## Interview Quick Revision

**What is the libuv Thread Pool?**
Worker threads used for certain expensive/blocking operations.

**Default size?**
4 threads.

**What happens when all workers are busy?**
Additional work waits for a free worker.

**Can the size change?**
Yes, using `UV_THREADPOOL_SIZE`.

**Is Node.js single-threaded?**
JavaScript execution is single-threaded, but libuv can use multiple worker threads.

**Does Node.js create one thread per request?**
No.

**What is ePoll?**
A Linux OS mechanism for scalable I/O event notification.

**ePoll vs Thread Pool?**
ePoll monitors I/O; Thread Pool provides workers for certain operations.

**What is a tick?**
One complete Event Loop cycle.

**Why avoid blocking the main thread?**
Because other callbacks and requests have to wait.

## Final Mental Model

```text
JavaScript → V8 → Main Thread
                  ↓
                libuv
              ↙      ↘
      Thread Pool    Event Loop / OS I/O
          ↓                ↓
    Worker Thread       ePoll / Sockets
          ↓                ↓
        Result          Callback
              ↘        ↙
              Call Stack
                  ↓
                  V8
```

> **Node.js keeps JavaScript execution on one main thread, while libuv uses worker threads and OS-level I/O mechanisms to handle work without unnecessarily blocking that thread.**
