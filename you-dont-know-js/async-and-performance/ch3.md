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

### Promise Trust









