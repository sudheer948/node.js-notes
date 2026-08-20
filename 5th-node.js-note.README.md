# Namaste Node.js — Episode 5: How Modules Work Behind the Scenes

## Overview

This episode goes deeper into how Node.js modules work internally. It explains **module privacy, the function wrapper, IIFE, `require()`, module caching, V8, libuv, and the actual Node.js source code**.

## 1. Why Are Module Variables Private?

Node.js wraps every module's code inside a **function wrapper** before executing it.

Because functions create their own scope, variables and functions inside one module remain private and don't automatically interfere with other modules.

```text
Module Code
    ↓
Function Wrapper
    ↓
Private Scope
    ↓
V8 executes it
```

This is why two modules can have variables with the same name without automatically conflicting.

## 2. IIFE

**IIFE = Immediately Invoked Function Expression**

An IIFE is a JavaScript function expression that executes immediately after being created.

Node.js uses this concept to explain its module wrapper and private module scope.

> IIFE is a JavaScript concept, not something specific to Node.js.

## 3. Where Do `require` and `module` Come From?

We can use:

```js
require("./file");
module.exports = something;
```

without declaring `require` or `module` ourselves.

Node.js provides them through the function wrapper around our module.

The wrapper receives important parameters:

```text
exports
require
module
__filename
__dirname
```

## 4. How `require()` Works

The episode explains `require()` using five major steps:

```text
Resolve → Load → Wrap → Evaluate → Cache
```

### 1. Resolve

Node.js determines what module or path is being requested.

### 2. Load

Node.js loads the appropriate content.

### 3. Wrap

JavaScript code is placed inside the Node.js function wrapper.

### 4. Evaluate

The module code executes and establishes `module.exports`.

### 5. Cache

The loaded module is stored in the cache.

The exported value is ultimately returned to the code that called `require()`.

## 5. Module Caching

Suppose:

```js
const xyz = require("./xyz");
```

loads `xyz.js` for the first time.

Node.js loads, wraps and evaluates it, then caches it.

If another file later does:

```js
require("./xyz");
```

Node.js can return the **cached module** instead of repeating the entire process.

This improves efficiency, especially in large applications with many repeated dependencies.

## 6. Node.js + V8 + libuv

Node.js prepares and wraps JavaScript module code before it is executed by **V8**.

* **V8** → JavaScript engine used by Node.js
* **libuv** → major Node.js runtime component involved in the event loop and multi-thread-related work
* **Node.js** → provides the runtime APIs and module system

The episode also demonstrates that APIs such as `setTimeout()` have real implementation code behind them.

## 7. `require()` Internally

The actual `require()` function is implemented inside the Node.js source code.

The episode follows an internal function called:

```text
makeRequireFunction
```

which creates and returns the `require` function used by modules.

The internal flow includes:

```text
makeRequireFunction
        ↓
module.require
        ↓
resolution
        ↓
cache check
        ↓
module.load
```

You don't need to memorize these internal functions. The important part is understanding how they relate to the high-level `require()` process.

## 8. Different File Types

When a module isn't cached, Node.js loads it from the file system.

Different extensions have different handling:

```text
.js    → JavaScript
.json  → JSON
.node  → Native Node.js module
```

JavaScript files then go through the compile/wrapper process before execution.

## 9. The Node.js Module Wrapper

Node.js creates a function wrapper around JavaScript module code.

Conceptually:

```js
(function (
  exports,
  require,
  module,
  __filename,
  __dirname
) {
  // Your module code
});
```

This wrapper creates the module's **private scope** and explains why these Node.js-specific variables are available automatically.

## 10. `__filename` and `__dirname`

### `__filename`

Gives the **full path of the current module file**.

### `__dirname`

Gives the **directory path of the current module**.

Both are supplied through the Node.js module wrapper.

## 11. Complete Mental Model

When Node.js loads a CommonJS module:

```text
Module Source
     ↓
require()
     ↓
Resolve
     ↓
Check Cache
     ↓
Load
     ↓
Compile / Prepare
     ↓
Wrap
     ↓
Evaluate
     ↓
module.exports
     ↓
Cache
     ↓
Return exports
```

V8 then executes the resulting JavaScript.

## 12. Why Read Node.js Source Code?

One of the biggest lessons from this episode is to develop **engineering curiosity**.

Instead of only asking:

* What does this API do?
* How do I use it?

also ask:

* Why does it work?
* How does it work?
* Where is it implemented?
* What happens internally?

Node.js is open source, so developers can inspect its actual implementation. The goal isn't to memorize the entire repository, but to become comfortable exploring source code when deeper understanding is needed.

## Interview Quick Revision

**Why are Node.js module variables private?**
Because Node.js wraps module code inside a function, creating a separate scope.

**What is IIFE?**
Immediately Invoked Function Expression.

**Where do `require` and `module` come from?**
Node.js supplies them through the module wrapper.

**What are the five steps of `require()`?**

```text
Resolve → Load → Wrap → Evaluate → Cache
```

**Why does Node.js cache modules?**
To avoid repeatedly loading and executing the same module.

**What is V8?**
The JavaScript engine used by Node.js.

**What is libuv?**
A major Node.js runtime component involved in the event loop and multi-thread-related work.

**What parameters are provided to the module wrapper?**

```text
exports
require
module
__filename
__dirname
```

**What is `__filename`?**
The full path of the current module.

**What is `__dirname`?**
The directory path of the current module.

## Key Takeaways

* Node.js wraps module code inside a function.
* The wrapper creates private module scope.
* IIFE means **Immediately Invoked Function Expression**.
* Node.js provides `require`, `module`, `exports`, `__filename`, and `__dirname`.
* `module.exports` exposes values from a CommonJS module.
* `require()` follows **resolve → load → wrap → evaluate → cache**.
* Modules are cached after being loaded.
* Cached modules don't need to be fully loaded and executed again.
* V8 executes JavaScript.
* libuv is a major part of Node.js runtime infrastructure.
* Node.js is open source, so its internal implementation can be inspected.
* You don't need to memorize Node.js source code; understand the mechanism and learn how to explore it.

### One-Line Mental Model

> **Node.js wraps every CommonJS module in a function to create private scope, provides Node-specific parameters, and uses `require()` to resolve, load, evaluate, cache, and return `module.exports`.**
