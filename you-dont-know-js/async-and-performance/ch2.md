# Callbacks

### Continuations
- callback function wraps/encapsulates ontinuation of the program
- get enough callbacks in a program and it's hard to intuitively understand the order your program will fire in

### Sequential Brain
- brains like plan events to be linearly
  - e.g. do A, then B, then C
- callbacks are not expressed step-by-step (in asynchronous code)
- "Hell is not understanding my own code"
  - believes callbacks are the main reason people don't understand their JS code
- nested callback chains make code hard to read but it's the uncertain nature of when things fire that makes it hard to understand
  - could be solved with hardcoding but this makes code brittle and less reusable

### Trust Issues
- inversion of control
  - control over code execution is given over to another (often 3rd) party
- risky to rely on 3rd party code to execute your code in a callback
  - how many times do they make the callback?
  - what if there's an error?
  - what if the callback fires too early/late?
- SIDE NOTE: Never wrap critical functionality inside a 3rd party analytics call...that's dumb!
- your code callbacks are risky too!
  - callbacks don't offer much functionality for guarding the borders/hinterlands

### Trying to Save Callbacks
- split design with a branch for failure and a branch for success
  - failure handler is usually optional and if you don't specify it, the assumption is you want the errors swallowed
  * this is the design used by ES6 promises
- error first/node style
  - first argument is reserved for error object (if any)
    - if no errors, this is set to empty/falsy
    - if error, this is true and nothing else happens
- these still have issues
  - nothing prevents multiple invocations of callback
  - could get both/neither of the success/error signals
  - very verbose
- to protect against 'never called' you'll need to setup a timeout to cancel the event
- to protect against will it or won't it async you'll have to wrap it in functions to force asynchronicity
- Don't worry, ES6 will save us all with promises
