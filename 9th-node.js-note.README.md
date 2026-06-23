✨ Pattern

libuv Internals + Event Loop + Callback Queues + Event Loop Phases + process.nextTick() + Promise Queue + setTimeout() + setImmediate() + Poll Phase + Advanced Output Questions

💡 Idea

This episode explains the actual brain of Node.js:

Node.js
   ↓
libuv
   ↓
Event Loop
   ↓
Callback Queues
   ↓
Asynchronous Execution

Previous episodes taught:

V8
 ↓
Offload Async Work
 ↓
libuv

This episode answers:

After libuv gets the work,
how are callbacks executed?

The answer is:

Event Loop
      +
Callback Queues

🔥 Episode Flow
1. libuv Components
        ↓
2. Callback Queues
        ↓
3. Event Loop
        ↓
4. Event Loop Phases
        ↓
5. Timer Phase
        ↓
6. Poll Phase
        ↓
7. Check Phase
        ↓
8. Close Phase
        ↓
9. process.nextTick
        ↓
10. Promise Queue
        ↓
11. Queue Priorities
        ↓
12. Output Questions
        ↓
13. Poll Waiting
        ↓
14. Nested nextTick

📘 Chapter 1: libuv Components ⭐⭐⭐⭐⭐

Akshay explains that libuv consists mainly of:

Diagram
libuv
 ├── Event Loop
 ├── Callback Queues
 └── Thread Pool
Explanation

libuv is not a single mechanism.

It contains:

Event Loop
Multiple callback queues
Thread Pool

This episode mainly focuses on the first two.

📘 Chapter 2: Why libuv Exists ⭐⭐⭐⭐⭐
Diagram
V8
 ↓
Async Task Found
 ↓
libuv
 ↓
Handle Task
Explanation

When JavaScript encounters:

fs.readFile()
https.get()
setTimeout()

V8 delegates those operations to libuv.

📘 Chapter 3: Callback Waiting Problem ⭐⭐⭐⭐⭐

Suppose:

API Response Ready

but

JavaScript Still Busy

What happens?

Diagram
Callback Ready
       ↓
Cannot Execute Yet
       ↓
Wait Somewhere
Explanation

Callbacks cannot interrupt running JavaScript.

They must wait until the Call Stack becomes available.

📘 Chapter 4: Callback Queues ⭐⭐⭐⭐⭐
Diagram
Async Task Complete
          ↓
Callback Queue
          ↓
Wait
Explanation

Completed callbacks are placed inside queues until execution becomes possible.

📘 Chapter 5: Multiple Callback Queues ⭐⭐⭐⭐⭐

One of the most important ideas.

Diagram
Timer Queue

Poll Queue

Check Queue

Close Queue
Explanation

Node.js does not use one giant queue.

Different callback types have different queues.

📘 Chapter 6: Event Loop Introduction ⭐⭐⭐⭐⭐

The hero of the episode.

Diagram
Callback Queues
        ↑
        |
   Event Loop
        |
        ↓
Call Stack
Explanation

The Event Loop continuously monitors:

Call Stack
Callback Queues

and moves callbacks when execution becomes possible.

📘 Chapter 7: Event Loop Job ⭐⭐⭐⭐⭐
Diagram
Call Stack Empty?
        ↓
Yes
        ↓
Move Callback
        ↓
Execute
Explanation

The Event Loop's main responsibility is:

Queue
  ↓
Call Stack
📘 Chapter 8: Equivalent Terms ⭐⭐⭐⭐

Akshay repeatedly says these mean almost the same thing:

Diagram
Call Stack Empty

JS Engine Idle

Main Thread Free
Explanation

All indicate that callbacks can now be executed.

📘 Chapter 9: Event Loop Phases ⭐⭐⭐⭐⭐

Most important concept.

Diagram
Timer
  ↓
Poll
  ↓
Check
  ↓
Close
  ↓
Repeat
Explanation

The Event Loop runs in phases.

It does not execute callbacks randomly.

📘 Chapter 10: Timer Phase ⭐⭐⭐⭐⭐
Diagram
Timer Phase
      ↓
setTimeout()
setInterval()
Explanation

Timer-related callbacks execute here.

📘 Chapter 11: Poll Phase ⭐⭐⭐⭐⭐

Most important phase.

Diagram
Poll Phase
      ↓
I/O Callbacks
      ↓
fs.readFile()
https.get()
Incoming Requests
Explanation

Most I/O operations complete here.

📘 Chapter 12: Check Phase ⭐⭐⭐⭐⭐
Diagram
Check Phase
      ↓
setImmediate()
Explanation

Callbacks registered through:

setImmediate(...)

execute in this phase.

📘 Chapter 13: Close Phase ⭐⭐⭐⭐
Diagram
Close Phase
      ↓
Cleanup Work
Explanation

Handles cleanup-related callbacks such as socket closing.

📘 Chapter 14: Event Loop Cycle ⭐⭐⭐⭐⭐
Diagram
Timer
 ↓
Poll
 ↓
Check
 ↓
Close
 ↓
Timer
 ↓
Poll
 ↓
Check
Explanation

This cycle repeats continuously.

📘 Chapter 15: process.nextTick() ⭐⭐⭐⭐⭐

One of the most important interview topics.

Diagram
process.nextTick()
         ↓
Special Queue
Explanation

Node.js gives process.nextTick special treatment.

It has higher priority than Event Loop phases.

📘 Chapter 16: Promise Queue ⭐⭐⭐⭐⭐
Diagram
Promise Resolved
        ↓
Promise Queue
Explanation

Promise callbacks have their own queue.

📘 Chapter 17: Priority Order ⭐⭐⭐⭐⭐

Must memorize.

Diagram
process.nextTick
       ↓
Promise Queue
       ↓
Timer
       ↓
Poll
       ↓
Check
       ↓
Close
Explanation

This is the execution priority used by Node.js.

📘 Chapter 18: First Output Question ⭐⭐⭐⭐⭐

Code contains:

setImmediate()
fs.readFile()
setTimeout(0)

Output:

100
Last Line
Timer Expired
Set Immediate
File Reading Callback
Explanation

File reading takes time.

When Event Loop reaches Check Phase:

setImmediate()

is already ready.

File reading is not.

Therefore:

setImmediate
     ↓
Before
     ↓
File Callback

📘 Chapter 19: Event Loop Runs Extremely Fast ⭐⭐⭐⭐
Diagram
Nanoseconds
      ↓
Microseconds
      ↓
Execution
Explanation

All these queue checks happen extremely quickly.

📘 Chapter 20: Mixed Priority Example ⭐⭐⭐⭐⭐

Code includes:

process.nextTick()
Promise.resolve()
setTimeout(0)
setImmediate()
fs.readFile()

Purpose:

To test queue priorities.

📘 Chapter 21: Why Sync Code Prints First ⭐⭐⭐⭐⭐
Diagram
Top-Level Code
       ↓
Runs Completely
       ↓
Callbacks Later
Explanation

Callbacks cannot run while top-level JavaScript is executing.

📘 Chapter 22: Output Of Mixed Example ⭐⭐⭐⭐⭐

Output:

A = 100
Last Line

process.nextTick

Promise

Timer Expired

Set Immediate

File Reading Callback
Explanation

Priority order controls execution.

📘 Chapter 23: Poll Waiting Behavior ⭐⭐⭐⭐⭐

One of the hardest concepts.

Diagram
No Work Available
        ↓
Wait At Poll Phase
Explanation

If:

Call Stack empty
Queues empty
No immediate work available

Node waits at Poll Phase.

📘 Chapter 24: Browser vs Node Event Loop ⭐⭐⭐⭐⭐
Diagram
Browser Event Loop
          ≠
Node.js Event Loop
Explanation

Do not assume browser behavior applies to Node.js.

Implementations differ.

📘 Chapter 25: Semi-Infinite Loop ⭐⭐⭐⭐
Diagram
Work Exists?
     ↓
Yes → Continue

No → Wait
Explanation

Node Event Loop can pause while waiting for work.

This is why some people call it:

Semi-Infinite Loop (it waits at the poll phase)
📘 Chapter 26: Advanced Poll Example ⭐⭐⭐⭐⭐

Code contains:

fs.readFile(...)

inside which new callbacks are scheduled:

setTimeout()
setImmediate()
process.nextTick()

Purpose:

Understanding nested scheduling.

📘 Chapter 27: Event Loop Does NOT Restart ⭐⭐⭐⭐⭐

One of the most important concepts.

Diagram
Poll Phase
     ↓
Execute Callback
     ↓
Continue Forward
Explanation

After Poll executes:

Event Loop continues from its current position.

It does not jump back to the beginning.

📘 Chapter 28: Nested Callback Scheduling ⭐⭐⭐⭐⭐
Diagram
File Callback
      ↓
Schedules

nextTick
setTimeout
setImmediate
Explanation

Callbacks can create new callbacks.

These join their respective queues.

📘 Chapter 29: Poll → Check Relationship ⭐⭐⭐⭐⭐
Diagram
Poll
 ↓
nextTick
 ↓
Promise
 ↓
Check
Explanation

After Poll completes:

Event Loop continues according to phase order.

📘 Chapter 30: Nested process.nextTick ⭐⭐⭐⭐⭐

Example:

process.nextTick(() => {
   process.nextTick(...)
})
Diagram
nextTick
    ↓
Creates nextTick
    ↓
Execute Again
Explanation

Node drains the nextTick queue completely before moving on.

📘 Chapter 31: Queue Draining Rule ⭐⭐⭐⭐⭐
Diagram
nextTick Queue
       ↓
Execute All
       ↓
Move Forward
Explanation

Event Loop does not partially process nextTick callbacks.

It empties the entire queue.

📘 Chapter 32: Final Advanced Output Example ⭐⭐⭐⭐⭐

Output:

Last Line

nextTick

Inner nextTick

Promise

Timer Expired

Set Immediate

File Reading Callback
Explanation

Nested nextTick gets executed before Event Loop proceeds.

📘 Chapter 33: Practice Recommendation ⭐⭐⭐⭐

Akshay repeatedly recommends:

Pause
Predict
Run
Verify
Explanation

Event Loop understanding comes through practice.

📘 Chapter 34: Preview Of Next Episode ⭐⭐⭐⭐⭐

Topics coming next:

Diagram
Thread Pool
      ↓
Thread Pool Size
      ↓
Single Threaded?
      ↓
Multi Threaded?
Explanation

The next episode completes libuv by covering Thread Pools.

⚠️ Tricky Points
Node uses multiple callback queues.
process.nextTick has highest priority.
Promise callbacks execute after nextTick.
Poll Phase handles I/O callbacks.
setImmediate executes in Check Phase.
Event Loop can wait at Poll Phase.
Event Loop does not restart after Poll callbacks.
nextTick queue must completely drain before moving on.
❌ Mistakes To Avoid

❌ Thinking all callbacks use one queue.

❌ Thinking Promise callbacks execute before process.nextTick.

❌ Thinking Poll callbacks always execute before setImmediate.

❌ Thinking Event Loop restarts from Timer Phase after every callback.

❌ Confusing Browser Event Loop with Node.js Event Loop.

❌ Ignoring nested nextTick behavior.

🎯 Important Interview Questions
What are the major components of libuv?
What is the Event Loop?
Why are callback queues required?
What are the Event Loop phases?
What happens in Timer Phase?
What happens in Poll Phase?
What happens in Check Phase?
What is setImmediate()?
What is process.nextTick()?
What is the Promise Queue?
What is the priority order in Node.js?
Why does process.nextTick run before Promises?
What happens when nextTick schedules another nextTick?
Does Event Loop restart after Poll?
Why does Node wait at Poll Phase?
What is a semi-infinite loop?
How is Node's Event Loop different from the browser's?
Why can setImmediate execute before fs.readFile callback?
⭐ Episode Rating

10/10

This is one of the most important Node.js internals episodes.

💼 Interview Importance

10/10

Contains extremely common Node.js interview questions:

Event Loop
process.nextTick
Promise Queue
setImmediate
Poll Phase
Output Questions
🚀 Job Readiness Impact

10/10

After this episode you understand:

✅ Event Loop Internals
✅ Callback Queues
✅ Event Loop Phases
✅ Timer Phase
✅ Poll Phase
✅ Check Phase
✅ Close Phase
✅ process.nextTick()
✅ Promise Queue
✅ Queue Priorities
✅ setImmediate()
✅ Poll Waiting Behavior
✅ Nested nextTick Execution
✅ Advanced Output Questions

This episode is the foundation for answering almost every Node.js Event Loop interview question confidently.
