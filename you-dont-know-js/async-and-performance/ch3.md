# You Don't Know JS - Async and Performance

## Chapter 3: Promises (p51)

Two major downsides to callbacks (discussed in Ch2):  
1. Lack of sequentiality - bad for expressing asynchrony
2. Lack of trustability - bad for managing concurrency

Inversion of control: handing callback over to something else and just "trusting" it to invoke as expected. Not great. Better if we had more control over flow.

Better pattern? PROMISES

### What is a Promise? (p52)

PROMISES:
- control over program flow (makes it predictable)
- returns when task finishes w/ resolve (success) or reject (failure)
- confirms when done, then we can tell code what to do next

Understand what a Promise is before looking at the code.

**Q:** Agree? Any reason to look at the code first?

### Future Value (p52-53)

BURGER PARTY EXAMPLE  
See also: http://kosamari.com/notes/the-promise-of-a-burger-party

Transaction flow:

1. Make a request
2. Receive _Promise_ of a future value
3. Time passes (other stuff can happen)
4. When ready, two possibilities:
  a. Receive actual value (future value resolves into present value)
  b. Receive error message (future value rejected)

### Values Now and Later (p53-55)

Operating on any variable assumes variable is already "resolved". So we've been making assumptions about set/resolved values all along, in a way.

Promises "normalize then _now_ and _later_" - just make them both "later" aka async. Allows you to reason about values in a "time-independent" way.

### Promise Value (p 55-58)

`.then()` can take two functions, first for resolve (success) and second for reject (failure).

**Q:** ^^ Better than using `.catch()`?

Fun fact: Promises are externally immutable.

### Completion Event (p58-61)

Using resolution of a Promise as a "flow-control mechanism" for multi-step asynchronous task:
- gives us nicer separation of concerns
- called function doesn't need to be aware of resolution/rejection
- almost like an event subscription (pub/sub)
- "uninversion of control" (blegh) - restoring control to calling code
- "neutral third-party negotiation"

### Promise "Events" (p61-64)

Promise rejection/resolution aren't technically "events", but they behave like events.

`.then(0)` registers fullfillment and/or rejection "events".

"The revealing constructor" pattern:
- pass in two params (resolve and reject, aka resolution functions)
- first signals success
- second signals failure

Caution: be careful chaining `.then()`s. It's actually a different pattern: "splitting/forking".

### Thenable Duck Typing (p64-66)

!!! You can receive a Promise form another browser window/frame.

**Q:** What? How?!

Basically, you can't rely on type-checking for Promises bc lots of fun edge cases. So lean on duck-typing instead (?) - - - concept of "thenable".

**Q:** What's an real world example of a "non-genuine" Promise?

> If you try to fulfill a Promise with any object/function value that
> happens to have a then(..) function on it, but you weren’t intending
> it to be treated as a Promise/thenable, you're out of luck...

^^ Why would you ever try to do this?

**A:** (p 66) There are several well-known non-Promise libraries prior to ES6 that have `.then()` method.

### Promise Trust (p 67)

Things Promises take care of:
- Calling callback too early
- Calling callback too late (or never)
- Calling callback too few or too many times
- Failing to pass along any necessary environment/parameters
- Swallowing any errors/exceptions that may happen

tl;dr: handles race conditions.

### Promise Scheduling Quirks (p68-)

> ...there are lots of nuances of scheduling where the relative
> ordering between callbacks chained off two separate Promises is
> **not reliably predictable.**

Wait...

> ...you should never rely on anything about the ordering/scheduling
> of callbacks across Promises. I

**Q:** ^^ I thought that was the whole point of using them? Pretty major point, at least.

> In fact, a good practice is not to code in such a way where the
> ordering of multiple callbacks matters at all. Avoid that if you can.

**Q:** ^^ Is he joking? That's a joke, right?

### Never Calling the Callback (p69-70)

Pretty sweet:

> ...nothing (not even a JS error) can prevent a Promise from
> notifying you of its resolution (if it’s resolved).

**Q:** What's his actually recommendation / solution here? How do you prevent program from hanging indefinitely?

### Trustable Promise (p73-74)

> But why would this be any more trustable than just callbacks alone?
> How can we be sure the something we get back is in fact a trustable
> Promise? Isn’t it basically all just a house of cards where we can
> trust only because we already trusted?

^^ Great question. Nice feature is they normalize any "thenable" args that get passed. Promises accept any "thenable". So pass any async stuff through a Promise for more trustworthy results.

### Chain Flow (p76-84)

Discussion topic: achieving Promise-aware async flow control w/ utilities like `ajax()` that expect callbacks.

> Although the native ES6 Promise mechanism doesn’t automatically
> solve this pattern for us, practically all Promise libraries do.
> They usually call this process “lift‐ ing,” “promisifying,” or
> some variation thereof.

> Intrinsic behaviors of Promises that enable chain flow control:
> - A then(..) call against one Promise automatically produces a new Promise to return from the call
> - Inside the fulfillment/rejection handlers, if you return a value or an exception is thrown, the new returned (chainable) Promise is resolved accordingly
> - If the fulfillment or rejection handler returns a Promise, it is unwrapped, so that whatever its resolution is will become the resolution of the chained Promise returned from the current then(..).

### Terminology: Resolve, Fulfill, and Reject (p84-)

Discussion point: "Resolve" vs "Fulfill"

**Q:** `reject()` doesn't unwrap like `resolve()` does... why not? Assuming you'll never get a Promise passed through to `reject()`?









