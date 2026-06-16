✨ Pattern

Installing Node.js + npm + Node REPL + JavaScript Runtime Environment + Running First Node.js Program + Global Object + globalThis + Browser vs Node.js Runtime

💡 Idea

This episode answers three very important questions:

1. How do we install Node.js?
2. How do we execute JavaScript using Node.js?
3. What is the Global Object inside Node.js?

The biggest takeaway:

Browser
    ↓
window

Node.js
    ↓
global

Universal Standard
    ↓
globalThis

And:

Node.js
    ↓
JavaScript Runtime Environment
    ↓
Executes JavaScript Using V8

This is the episode where you move from merely understanding Node.js architecture to actually writing and running code.

🔥 Episode Flow
1. Installing Node.js
         ↓
2. Node Version Verification
         ↓
3. npm Installation
         ↓
4. Node REPL
         ↓
5. Running JavaScript In Node
         ↓
6. JavaScript Runtime Environment
         ↓
7. Creating First Project
         ↓
8. VS Code Setup
         ↓
9. Running app.js
         ↓
10. Global Object
         ↓
11. Browser vs Node.js
         ↓
12. this Keyword Difference
         ↓
13. globalThis
         ↓
14. JavaScript Standardization
         ↓
15. Deep Learning Philosophy

📘 Chapter 1: Installing Node.js

To use Node.js:

Download
      ↓
Install
      ↓
Verify
      ↓
Start Coding

Official Source

Use:
Node.js Official Website

Installation Methods

Method 1

Using:
NVM
(Node Version Manager)

Method 2

Using:

Pre-built Installer

Download:

.pkg
.exe

and install normally.

📘 Chapter 2: Node Version Selection

Akshay recommends:

Latest Stable Version

or

LTS Version

Reason:

Stable
Supported
Production Ready

Avoid:

Very Old Versions

while following the course.

📘 Chapter 3: NVM (Node Version Manager)

NVM helps manage:

Multiple Node Versions

Example:

Project A
→ Node 16

Project B
→ Node 20

NVM allows easy switching.

📘 Chapter 4: Installation Problems Are Normal

One of Akshay's first developer lessons.

Possible Issues:

Wrong processor
Existing Node version
Environment conflict
OS-specific problem

Engineering Mindset
Error
 ↓
Google
 ↓
Stack Overflow
 ↓
Fix

Important lesson:
Problems Are Part Of Development

📘 Chapter 5: Verify Node Installation

Command:

node -v

Output:

v16.x.x
v20.x.x

etc.

Meaning:

Node Installed Successfully

If you get:

command not found

Node isn't installed correctly.

📘 Chapter 6: npm

Node automatically installs:

npm

along with itself.

Check Version:

npm -v

Definition:

Node Package Manager

Purpose:

Install packages
Manage dependencies
Manage projects

🎯 Interview Question

Does npm require separate installation?

Answer:

No

It comes with Node.js.

📘 Chapter 7: What Is Node REPL? ⭐⭐⭐

REPL stands for:

Read
Evaluate
Print
Loop

Command:
node

Result:
Interactive JavaScript Environment
REPL Flow
Read Code
      ↓
Evaluate
      ↓
Print Output
      ↓
Loop Again

Example
1 + 1

Output:

2

Variable Example:

var a = "Akshay";

Then:

a

Output:

"Akshay"

Arithmetic:

var i = 10;
var j = 20;

i + j

Output:
30

📘 Chapter 8: First Understanding Of Runtime

Inside REPL:

JavaScript Executes

How?

JavaScript
      ↓
Node.js
      ↓
V8 Engine
      ↓
Execution

This is why Node.js is called:
JavaScript Runtime Environment

📘 Chapter 9: Browser Console vs Node REPL

Very important comparison.

Browser
Chrome
  ↓
V8

Console:

1 + 1

works.

Node.js
Node.js
   ↓
V8

REPL:

1 + 1

works.

Key Insight
Same JavaScript
Different Runtime

📘 Chapter 10: Why REPL Isn't Enough

Problem:

No Project Structure

Need:

Folders
Files
Projects

Therefore:
Create Real Project

📘 Chapter 11: Creating First Node Project

Folder:
namaste-node

Contains:
app.js

Purpose:
Store Application Code

📘 Chapter 12: VS Code

Recommended Editor:
Visual Studio Code

Reasons:

✅ Free
✅ Popular
✅ JavaScript Friendly
✅ Large Ecosystem

Other editors also work.

📘 Chapter 13: First Node.js File

File:
app.js

Example:
var name = "Namaste Node.js";

var a = 10;
var b = 20;

console.log(name);
console.log(a + b);

📘 Chapter 14: Running JavaScript File ⭐⭐⭐

Command:
node app.js

Flow:
app.js
   ↓
Node.js
   ↓
V8
   ↓
Execution
   ↓
Output

Output:

Namaste Node.js
30

This is the first real Node.js program.

📘 Chapter 15: VS Code Terminal

Terminal can be:

VS Code Terminal
iTerm
Windows Terminal
Linux Terminal

Commands remain:
Exactly Same

📘 Chapter 16: How Node Executes Code

When:
node app.js

runs:
app.js
      ↓
Node.js
      ↓
V8
      ↓
Line By Line Execution

Because JavaScript is:
Single Threaded
Synchronous

📘 Chapter 17: Global Object In Browser ⭐⭐⭐

Browser provides:
window

Important:
window
≠ V8 Feature

It is:
Browser Feature

Provided by:

Chrome
Firefox
Safari

📘 Chapter 18: Global Object In Node.js ⭐⭐⭐

Node.js provides:
global

Example:
console.log(global);

Contains:

setTimeout
setInterval
setImmediate

and many other runtime APIs.

Important Insight
global
≠ V8 Feature

Instead:
global
=
Node.js Feature

One of Node's "superpowers".

📘 Chapter 19: Node.js Superpowers Revisited

Architecture:

Node.js
=
V8
+
Superpowers

Examples:

global
setTimeout
setInterval
setImmediate

These are not part of core ECMAScript.

📘 Chapter 20: this In Node.js ⭐⭐⭐

Question:
console.log(this);

Output:
{}

Not:
global

Browser
this === window
Node.js
this !== global

Very common interview question.

📘 Chapter 21: Global Object History

Different environments used different names.

Browser:
window

Web Workers:
self

Frames:
frames

Node.js:
global

Problem:
No Consistency

📘 Chapter 22: globalThis ⭐⭐⭐

One of the most important concepts.

To standardize:
globalThis
was introduced.

Purpose:
One Global Object
Across All JavaScript Runtimes

Works in:

Browser
Node.js
Web Workers

Why Not Use global?

Because:
Possible Naming Conflicts
with existing applications.

Therefore:
globalThis
was chosen.

📘 Chapter 23: globalThis In Node.js

Verification:
globalThis === global

Result:
true

Meaning:
Both Point To Same Object
Because objects are references.

📘 Chapter 24: Akshay's Biggest Message ⭐

The most important non-technical lesson.

Bad Developer:
Uses Things

Good Developer:
Understands Things

Great Developer:
Understands
Why Things Exist

Akshay repeatedly encourages:
Ask Why?
Read Open Source
Stay Curious
Learn Internals

🛠 Practical Examples
Check Node Version
node -v
Check npm Version
npm -v
Start REPL
node
Run File
node app.js
Global Object
console.log(global);
Universal Global
console.log(globalThis);

⚠️ Tricky Points
Node.js ≠ V8.
global ≠ V8 feature.
window exists only in browser.
this behaves differently in Node.js.
globalThis is the standard global object.
npm comes with Node.js.
REPL is not used for real project development.

❌ Mistakes To Avoid

❌ Thinking window exists in Node.js.

❌ Thinking global exists in browser.

❌ Confusing global with globalThis.

❌ Thinking this === global in Node.js.

❌ Using REPL as a project environment.

❌ Memorizing commands without understanding runtime concepts.

🎯 Important Interview Questions
Node.js
What is Node REPL?
What does REPL stand for?
How do you run a Node.js file?
What is npm?
Runtime
Why is Node.js called a runtime?
How does Node execute JavaScript?
Global Object
What is the global object in browser?
What is the global object in Node.js?
Is global part of V8?
Difference between window and global?
globalThis
Why was globalThis introduced?
What problem does it solve?
What does globalThis === global return in Node.js?
JavaScript Internals
Why does browser have window?
What role does TC39 play in JavaScript evolution?

⭐ Episode Rating
9.5/10

Not heavy on coding, but extremely important for understanding the Node.js runtime environment.

💼 Interview Importance

10/10

Contains common interview topics:

Node REPL
npm
Global Object
globalThis
Runtime Environments
Browser vs Node.js

🚀 Job Readiness Impact

9/10

After this episode you understand:

✅ Installing Node.js
✅ npm Basics
✅ Running Node Programs
✅ Node REPL
✅ Node Runtime Environment
✅ Global Object
✅ globalThis
✅ Browser vs Node.js Differences
✅ JavaScript Standardization Process

This episode strengthens your foundations before Node.js modules, imports/exports, and backend application development begin in the next episodes.
