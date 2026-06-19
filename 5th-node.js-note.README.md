✨ Pattern

How require() Works Internally + Module Wrapper + IIFE + Module Privacy + require() Lifecycle + Module Caching + Node.js Source Code Exploration + CommonJS Loader + Hidden Module Parameters

💡 Idea

This episode answers one of the biggest Node.js questions:

How Does require() Actually Work?

Most developers know:

require("./sum");

But very few know what happens internally.

The biggest takeaway:

Module Code
      ↓
Node.js Wraps It
      ↓
IIFE / Wrapper Function
      ↓
Injects require, module, exports
      ↓
Executes Code
      ↓
Caches Result

This episode is less about writing code and more about understanding the internals of Node.js.

🔥 Episode Flow
1. Module Privacy
          ↓
2. Function Scope Revision
          ↓
3. IIFE
          ↓
4. Module Wrapper
          ↓
5. require() Internals
          ↓
6. Wrapper Parameters
          ↓
7. require() Lifecycle
          ↓
8. Module Resolution
          ↓
9. Loading
          ↓
10. Compilation
          ↓
11. Evaluation
          ↓
12. Caching
          ↓
13. Node.js Source Code
          ↓
14. CommonJS Loader
          ↓
15. setTimeout Source
          ↓
16. Hidden Parameters
          ↓
17. __filename
          ↓
18. __dirname
          ↓
19. Open Source Learning

📘 Chapter 1: The Big Question

Akshay starts with:

Why Are Variables
Private Across Modules?

and

What Actually Happens
When require() Runs?

These are the core questions of the episode.

📘 Chapter 2: Function Scope Revision

Example:

function x() {
   const a = 10;

   function b() {}
}

Important rule:

Variables Inside Function
Stay Inside Function

Outside code cannot access:

a

or

b
📘 Chapter 3: Module Privacy ⭐⭐⭐

Question:

Why Can't app.js Access
Everything Inside sum.js?

Answer:

Function Scope

Node.js uses function scope to create:

Module Privacy

📘 Chapter 4: IIFE ⭐⭐⭐

IIFE means:

Immediately
Invoked
Function
Expression

Example:

(function () {

})();

Flow:

Create Function
      ↓
Execute Immediately

Purpose:

Private Scope

📘 Chapter 5: Why IIFE?

Example:

Outside:

var a = 100;

Inside:

var a = 1000;

Result:

No Conflict

Because:

Separate Scope

exists.

📘 Chapter 6: Node's Module Wrapper ⭐⭐⭐⭐⭐

The most important concept of the episode.

Node internally wraps every module.

Mental model:

sum.js
      ↓
Wrapper Function
      ↓
Execution

This is the reason:

Module Privacy Exists

📘 Chapter 7: Where Does require() Come From?

Question:

Who Created require()?

Answer:

Node.js

It is not part of JavaScript itself.

Node injects it automatically.

📘 Chapter 8: Where Does module Come From?

Question:

module.exports

Who creates module ?

Answer:

Node.js

Node provides it during module execution.

📘 Chapter 9: Hidden Parameters ⭐⭐⭐

Node passes special parameters to every module.

Examples:

exports
require
module
__filename
__dirname

These become available automatically.

📘 Chapter 10: Internal Wrapper Structure

Conceptually:

(function(
 exports,
 require,
 module,
 __filename,
 __dirname
){

   // module code

});

Node wraps module code inside this structure before execution.

📘 Chapter 11: require() Lifecycle ⭐⭐⭐

Akshay explains the major stages.

Step 1
Resolve Module

Determine what was requested.

Examples:

JS File
JSON File
Folder
Core Module

Step 2
Load Module

Read file contents.

Step 3
Compile

Prepare code for execution.

Step 4
Evaluate

Execute code.

Step 5
Cache

Store result for reuse.

📘 Chapter 12: Module Resolution

Example:

require("./sum")

Node first resolves:

Where Is This File?

Then proceeds with loading.

📘 Chapter 13: Validation Inside require()

Example:

require("")

Node throws:

ID Must Be A Non-Empty String

Important lesson:

Errors Come From Real Source Code

📘 Chapter 14: Loading Modules

Node loads:

Actual File Contents

before execution.

Depending on extension:

.js
.json
.node

different handlers run.

📘 Chapter 15: Compile Step ⭐⭐⭐

After loading:

File Content
      ↓
Compile
      ↓
Wrapper Applied

This is where module code gets prepared.

📘 Chapter 16: Real Wrapper Discovery ⭐⭐⭐⭐⭐

Akshay finds the actual wrapper logic inside Node.js source.

Important realization:

Everything Taught Earlier
Is Real

The wrapper genuinely exists in source code.

📘 Chapter 17: String-Based Wrapping

Interesting observation.

Node builds wrapper using:

String Concatenation

Then inserts:

Module Code

between wrapper boundaries.

📘 Chapter 18: Module Caching ⭐⭐⭐

One of the most important backend concepts.

Scenario:

app.js
      ↓
requires xyz


sum.js
      ↓
requires xyz


multiply.js
      ↓
requires xyz

Question:

Will xyz.js Execute
Again And Again?

Answer:

No

Flow:

First Load
      ↓
Cache
      ↓
Reuse

📘 Chapter 19: Why Caching Exists?

Reason:

Performance

Avoids:

Repeated Loading
Repeated Execution

Makes applications faster.

📘 Chapter 20: Node.js Source Code Exploration ⭐⭐⭐

Akshay explores the actual Node.js repository.

Important realization:

Node.js
=
Open Source

Anyone can read the code.

📘 Chapter 21: setTimeout Exploration ⭐⭐⭐

Example:

setTimeout(() => {
   console.log("Hello");
}, 3000);

Question:

Who Implemented setTimeout?

Answer:

Node.js Developers

It is actual source code.

Not magic.

📘 Chapter 22: timers.js

Akshay explores:

timers.js

Important realization:

setTimeout
Is Exported
Like Normal Modules

📘 Chapter 23: Event Loop Preview

Brief mention.

Concepts previewed:

Event Loop
Callbacks
Timing

Not discussed deeply yet.

📘 Chapter 24: CommonJS Loader ⭐⭐⭐

Akshay explores:

CommonJS Loader

inside Node.js source.

This loader handles:

require()

internally.

📘 Chapter 25: helpers.js ⭐⭐⭐

Important file explored:

helpers.js

Contains logic involved in creating:

require()

functionality.

📘 Chapter 26: makeRequireFunction()

Important function:

makeRequireFunction()

Purpose:

Build require()

used by modules.

📘 Chapter 27: __filename ⭐⭐⭐

Example:

console.log(__filename);

Returns:

Full File Path

of current file.

📘 Chapter 28: __dirname ⭐⭐⭐

Example:

console.log(__dirname);

Returns:

Directory Path

of current module.

📘 Chapter 29: GitHub.dev Trick

Press:

.

inside GitHub repository.

Result:

GitHub
      ↓
VS Code Interface

Useful for code exploration.

📘 Chapter 30: Open Source Development

Akshay observes:

TODO comments
Contributors
Copyright notices
Ongoing development

Important realization:

Node.js Is Continuously Evolving

📘 Chapter 31: Curiosity Is The Superpower ⭐⭐⭐

One of the strongest messages.

Average Developer:

Uses APIs

Strong Developer:

Understands APIs

Excellent Developer:

Reads Internals

Questions to ask:

Why?
How?
What Happens Behind The Scenes?

🛠 Practical Examples
IIFE
(function () {
   console.log("Hello");
})();

Module Wrapper Idea
(function(
 exports,
 require,
 module,
 __filename,
 __dirname
){

 // module code

});

Invalid Require
require("");

Throws error because id must be non-empty.

File Path
console.log(__filename);
Directory Path
console.log(__dirname);
⚠️ Tricky Points
require() is not a JavaScript feature.
module is not a JavaScript feature.
Node injects hidden parameters.
Modules are wrapped before execution.
Module privacy comes from wrapper scope.
require() performs caching.
setTimeout is implemented by real source code.
CommonJS loading is synchronous.

❌ Mistakes To Avoid

❌ Thinking require() belongs to JavaScript.

❌ Thinking modules are magically isolated.

❌ Ignoring module caching.

❌ Assuming __filename and __dirname are global JavaScript features.

❌ Treating Node APIs as magic.

❌ Never reading documentation or source code.

🎯 Important Interview Questions
How does require() work internally?
Why are variables private across modules?
What is an IIFE?
Why does Node wrap modules?
What hidden parameters does Node provide?
What is module caching?
Why is caching important?
What are the steps of require()?
What does __filename return?
What does __dirname return?
Where does require() come from?
Where does module.exports come from?
How are CommonJS modules loaded?
Why does require("") throw an error?

⭐ Episode Rating

10/10

One of the deepest foundation episodes in Namaste Node.js.

💼 Interview Importance

10/10

Contains advanced Node.js internals that many developers know how to use but cannot explain.

🚀 Job Readiness Impact

9.5/10

After this episode, you understand:

✅ Module Wrapper
✅ IIFE
✅ Module Privacy
✅ require() Internals
✅ Module Caching
✅ CommonJS Loader
✅ __filename
✅ __dirname
✅ Open Source Exploration
✅ How Node.js Executes Modules

This episode doesn't make you build APIs yet, but it gives you a deep understanding of why Node.js modules behave the way they do. Many developers use require() every day; far fewer can explain what happens after they press Enter. This episode bridges that gap. 🚀
