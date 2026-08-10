# Node.js — Episode 1: Introduction & History

## What is Node.js?

**Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine that allows JavaScript to run outside the browser.**

### Key Concepts

* **JavaScript Runtime** → Environment where JavaScript executes.
* **V8 Engine** → JavaScript engine used by Chrome and Node.js.
* **Cross-platform** → Runs on Windows, Linux, macOS, Unix, etc.
* **Open source** → Maintained under the OpenJS Foundation.
* **Event-driven** → Node.js follows an event-driven architecture.
* **Non-blocking I/O** → Uses asynchronous/non-blocking I/O.

## Why Node.js?

Before Node.js, servers such as Apache commonly used a blocking approach. Ryan Dahl wanted a **non-blocking server** capable of handling multiple requests with fewer threads.

Node.js also allowed JavaScript to move beyond the browser into server-side and other environments.

## JavaScript Engines

Every environment that executes JavaScript needs a JavaScript engine.

| Environment | Engine       |
| ----------- | ------------ |
| Chrome      | V8           |
| Firefox     | SpiderMonkey |
| Node.js     | V8           |

Ryan Dahl initially used SpiderMonkey but switched to V8 during Node.js development.

## Node.js History

| Year     | Event                                                  |
| -------- | ------------------------------------------------------ |
| **2009** | Ryan Dahl created/released Node.js                     |
| **2009** | Initially used SpiderMonkey → switched to V8           |
| **2009** | Originally called **Web.js**                           |
| **2010** | npm introduced                                         |
| **2011** | Windows support added                                  |
| **2012** | Ryan Dahl stopped maintaining Node.js                  |
| **2014** | IO.js created as a fork                                |
| **2015** | Node.js + IO.js merged; Node.js Foundation formed      |
| **2019** | Node.js Foundation + JS Foundation → OpenJS Foundation |

## npm

**npm = package manager + registry for the Node.js ecosystem.**

It allows developers to **publish, share, and reuse packages** instead of building everything from scratch. npm became a major reason for Node.js's success.

## IO.js

**IO.js** was a fork of Node.js created in **2014** because of differences in development and release processes.

In **2015**, Node.js and IO.js merged, bringing the projects back together.

## Why Node.js Became Successful

1. JavaScript outside the browser
2. Powerful V8 engine
3. Non-blocking I/O
4. Event-driven architecture
5. Huge npm ecosystem
6. Cross-platform support

## Interview Quick Revision

**Q: What is Node.js?**
A: A JavaScript runtime built on Chrome's V8 engine that runs JavaScript outside the browser.

**Q: Which engine does Node.js use?**
A: V8.

**Q: Who created Node.js?**
A: Ryan Dahl.

**Q: When was Node.js released?**
A: 2009.

**Q: What was Node.js originally called?**
A: Web.js.

**Q: What is npm?**
A: The package manager and registry for the Node.js ecosystem.

**Q: Why was Node.js created?**
A: To provide a non-blocking approach to handling server requests.

**Q: What is IO.js?**
A: A fork of Node.js created in 2014.

**Q: When did Node.js and IO.js merge?**
A: 2015.

**Q: Who maintains Node.js today?**
A: The OpenJS Foundation.

## 🧠 Remember This

> **Node.js = JavaScript Runtime + V8 + Outside Browser + Event-driven + Non-blocking I/O + npm**

**Created by:** Ryan Dahl
**Released:** 2009
**Original name:** Web.js
**Current foundation:** OpenJS Foundation
