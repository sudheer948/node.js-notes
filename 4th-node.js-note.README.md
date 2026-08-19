# Namaste Node.js — Episode 4: Modules

## Overview

Node.js applications are divided into multiple **modules** instead of keeping all the code inside a single file. A module is a separate and private collection of JavaScript code.

The main concepts covered are:

* Modules
* `require()`
* `module.exports`
* CommonJS (CJS)
* ES Modules (ESM)
* Folder modules
* `index.js`
* JSON modules
* Node.js core modules

## CommonJS

CommonJS uses:

```js
const sum = require("./sum");
```

To expose functionality:

```js
module.exports = { calculateSum };
```

`require()` loads the module and returns whatever the module exposes through `module.exports`.

A module's variables and functions are **private by default**, so requiring a module does not automatically expose everything inside it.

## Exporting Multiple Values

Multiple values can be exported using an object:

```js
module.exports = {
  x,
  calculateSum
};
```

They can then be extracted using **object destructuring**:

```js
const { x, calculateSum } = require("./sum");
```

Object property shorthand makes `{ x, calculateSum }` possible when the property and variable names are the same.

## CommonJS vs ES Modules

| CommonJS                     | ES Modules                    |
| ---------------------------- | ----------------------------- |
| `require()`                  | `import`                      |
| `module.exports`             | `export`                      |
| Synchronous by default       | Asynchronous option available |
| Non-strict by default        | Strict by default             |
| Older/common Node.js pattern | Modern module pattern         |

ES Modules can be enabled in the demonstrated setup using:

```json
{
  "type": "module"
}
```

## Folder Modules

Related functionality can be grouped inside a folder:

```text
calculate/
├── sum.js
├── multiply.js
└── index.js
```

`index.js` can collect and export functionality from the internal modules.

Then the folder itself can be required:

```js
const calculate = require("./calculate");
```

This hides the internal file structure and provides a simpler interface to the rest of the application.

## Other Important Concepts

* `.js` can be omitted when requiring JavaScript modules.
* `require()` can import JSON files.
* `module.exports` starts as an empty object.
* You can replace `module.exports` or attach properties to it.
* Node.js provides built-in **core modules**, such as `util`.

## Key Takeaway

> **Node.js modules provide separate private scopes for JavaScript code, while CommonJS allows modules to communicate explicitly using `require()` and `module.exports`.**

Understanding modules is essential for organizing larger Node.js applications and is also an important interview topic.
