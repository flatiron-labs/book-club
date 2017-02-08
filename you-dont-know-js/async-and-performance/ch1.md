# Asynchrony: Now & Later

### A Program in Chunks
- If we synchronously execute code that relies on another system (i.e. requests, etc.), it will block the rest of the code from running and can block the DOM.
- Instead use asynchronous code so that when the code that relies on another system is resolved, additional code can be run at this time.
- Think of a _now_ chunk of code and a _later_ chunk of code.

### Async Console
- Based on the brower, some will defer the execution of `console.log` (async) so it might give you unexpected results.
- The best way to debug is to throw breakpoints in your code.

### Event Loop
- Until ES6, JS didn't have a notion of running code asynchronously. It has been mostly implemented in hosting envirnoments like the browser. It uses an Event Loop that schedules chunks of code to be executed at the correct moment.
- The Event Loop can be conceptualized as a queue (FIFO) that is in an infinite loop. When an event is "asynced", it is inserted into the loop.
- Since the Event loop can have many tasks queued up, `setTimeout` doesn't guarantee an exact execution time. Just that it will wait at least _x_ time until it is put into the Event Loop.

### Parallel Threading
- Async = gap between doing something now and later
- Parallel = doing multiple things at the same time
- JS never shares data across threads so we don't have to concern ourselves with issues that arise from multi-threading
- One case in which JS is not determinitstic is when callbacks share data and the data is mutated in the callbacks. Which callbacks fires first is not always the same.

### Run-to-Completion
- JavaScript will always finish running a chunk of code in its entirety before starting the next (even in cases when 2 requests have callbacks. Which ever fires first will run-to-completion before the next runs)

### Concurrency
- Concurrency is when 2 or more "processes" are executing simultaneously in the same period.
  - This is unrelated to parallel execution, which is operations happening at the same instant on seperate processors.
- I'm really unclear of what this has to do with stuff...

### Noninteracting
- When concurrent code doesn't interact with each other.
- Things happen as expected

### Interaction
- When concrrent code interact with each other, race conditions occur and you run into bugs.
  - Try to avoid writing code that has interaction when the order of execution is non-deterministic.
- A technique to avoid something from firing too early in race conditions is called a _gate_ where you can use a condition to make sure all events have fired before running a piece of code.
- Another called _latch_ is when only 1 event wins the race condition.
  - _2 is not a winner and 3 no body remembers_ - Nelly

### Cooperation
- The goal is to take a long running "process" and break it into steps or batches.
- You could use `setTimeout` to batch loops on large collections into several event loops so it doesn't block to code
- Anywhere this could apply for Learn? (track nav? track switcher?)

### Jobs
- ES6 introduces Job queue. It does not have an exposed API to interact directly with it.
- Imagine in an event loop tick, you want to have something happen at the end of the current event loop tick before the next event loop tick. That's where we use Job queue.
- Job queue is compareable to `setTimeout(..0)` but more controlled.

### Statement Ordering
- JS Engines might reorder statements in your code for optimizations, but you should never see any observable change from the code execution (except maybe performance)
