# Namaste Node.js — Episode 3

## 1. Installing Node.js

Node.js needs to be installed before writing and executing Node.js programs.

Common installation methods:

* **NVM (Node Version Manager)** — used to install and manage multiple Node.js versions.
* **Pre-built installer** — download and install Node.js for your operating system.

After installation, verify it using:

```bash
node -v
npm -v
```

* `node -v` → checks the Node.js version.
* `npm -v` → checks the npm version.
* npm is installed along with Node.js.

---

## 2. Node REPL

**REPL** stands for:

> Read → Evaluate → Print → Loop

The Node REPL provides an interactive environment where JavaScript can be executed directly from the terminal.

Start it with:

```bash
node
```

You can then test JavaScript expressions:

```js
1 + 1
```

REPL is mainly useful for **quick experiments and testing**, not for building complete production applications.

---

## 3. Running JavaScript with Node.js

For real applications, JavaScript is normally written inside files.

Example:

```text
project/
└── app.js
```

Run the file using:

```bash
node app.js
```

When `node app.js` is executed:

1. Node.js reads the JavaScript code.
2. Node.js passes the JavaScript to the **V8 engine**.
3. V8 executes the JavaScript.
4. The program produces its output.

---

## 4. Node.js and V8

An important concept is understanding the difference between **V8** and **Node.js**.

### V8

V8 is a **JavaScript engine** that executes JavaScript according to ECMAScript.

### Node.js

Node.js is a **JavaScript runtime environment** that:

* Uses V8 to execute JavaScript.
* Provides additional runtime capabilities.
* Allows JavaScript to run outside the browser.

Think of it as:

```text
JavaScript
    ↓
   V8
    ↓
 Node.js Runtime
    ↓
Additional runtime capabilities
```

---

## 5. Global Objects

Different JavaScript environments provide different global objects.

### Browser

```js
window
```

The browser provides `window` as its global object.

### Node.js

```js
global
```

Node.js provides `global` as its global object.

For example, Node.js provides functionality such as:

```js
setTimeout()
setInterval()
setImmediate()
```

These runtime capabilities are provided by Node.js rather than being part of the V8 engine itself.

---

## 6. `this` in Node.js vs Browser

The behavior of `this` can differ between environments.

In the browser, `this` can refer to the `window` global object in the relevant global context.

In the Node.js file context demonstrated in the episode, logging `this` produces an empty object rather than the Node.js `global` object.

Therefore:

> Don't assume that `this`, `window`, and `global` behave identically in every JavaScript environment.

---

## 7. `globalThis`

JavaScript runs in many different environments, and historically different environments used different names for their global object:

```text
Browser      → window
Web Worker   → self
Browser      → frames
Node.js      → global
```

To provide a standardized way to access the global object, JavaScript introduced:

```js
globalThis
```

`globalThis` works across different JavaScript environments, including browsers, Node.js, and web workers.

In Node.js:

```js
globalThis === global
```

produces:

```text
true
```

This means both refer to the same global object.

---

## 8. Important Interview Questions

### What is Node REPL?

Node REPL is an interactive environment for quickly executing JavaScript.

**REPL = Read, Evaluate, Print, Loop.**

### How do you start Node REPL?

```bash
node
```

### How do you execute a JavaScript file?

```bash
node app.js
```

### Is REPL used for production applications?

No. It is mainly useful for quick experiments and testing. Production applications are normally organized into files and projects.

### What is the global object in a browser?

```js
window
```

### What is the global object in Node.js?

```js
global
```

### What is `globalThis`?

`globalThis` is the standardized way to access the global object across different JavaScript runtime environments.

### What is the difference between V8 and Node.js?

**V8** is the JavaScript engine that executes JavaScript.

**Node.js** is the runtime environment that uses V8 and adds additional runtime-specific capabilities.

---

## 9. Key Takeaways

* Node.js allows JavaScript to run outside the browser.
* Node.js uses the **V8 JavaScript engine**.
* `node` starts the Node REPL.
* REPL means **Read, Evaluate, Print, Loop**.
* `node app.js` executes a JavaScript file.
* `node -v` checks the Node.js version.
* `npm -v` checks the npm version.
* Browser global object → `window`
* Node.js global object → `global`
* Node.js provides APIs such as `setTimeout`, `setInterval`, and `setImmediate`.
* `globalThis` provides a standardized way to access the global object.
* In Node.js, `globalThis === global` is `true`.
* **V8 is the engine; Node.js is the runtime environment around it.**

### Core Concept

> **Node.js is a JavaScript runtime environment that uses V8 to execute JavaScript and adds runtime-specific capabilities such as the Node.js global object and its APIs.**
