# Chapter 7 Releasing

1. Done Done - Steven 1
2. No bugs 3
3. Version Control - 0
4. Ten-Minute Build - 2
5. Continuous Integration - 2
6. Collective Code Ownership - 
7. Documentation - .5

## 1. "Done Done"
  - done when production ready software
  - Best Practices
    - use TDD.
    - show screens to customers throughout, not just at the end of an interation so they can make changes
    - fix bugs right away
    - when story is done, show it to customers for final acceptance review
    - **make stories small enough that you can complete them in a single week**
    - make stories smaller by splitting them into multiple parts
    - don't inflate your velocity or take credit if it's not really done
    - spread out wrap-up and polish work throughout the iteration

**Questions**:
  - How should we handle tickets that are "mostly" done? 
  - Does it make sense to have an "Acceptance" column for top-level user stories or epics?
  - "You are in control of the schedule." This doesn't seem to be the case now in certain situations...how do we think about program launches that have arbitrary dates?
  
## 2. No bugs
- book promises that you generate fewer defects under agile
- start with TDD, work normal hours, pair program
- eliminate bug breeding grounds
  - pay down tech debt in small chunks, refactor as you go
  - fix bugs now
    - write a test to make the bug obvious
    - identify systemic problems and share them at stand up
    - if you can't fix it immediately, write it down and come back to it. if it's pretty big, talk to product about whether to include it in release plan
    - fix your process with root cause analysis
  - Controversial: "All else remaining equal, experienced developers will always produce better results and more quickly than novices. If you have the option to bring high-quality people into your team, do it."
    
**Questions:**
  - I was a little offended by this last sentiment about hiring. I think junior people ask questions that can reveal logical flaws. What do we think?
  - A lot of this seemed straightforward. When do you think something is too deep in tech debt to tackle in the iteration? ex) curriculum
  - How should we think about and communicate the cost/value proposition of certain bugs? 
    
## 3. Version Control
  - less important w/ github? did people just not use version control in the past?
  - what about bigger picture problems? how to integrate multiple times per day? 
  - store the entire project in a single repository (including source, documentation)
  - customer data including docs, notes on requirements, technical writing, and tests should go in there too)

**Questions:**
  - "Single Codebase" section -- why would you ever dupliate the codebase?? Would this be like a white label situation?
  - Is there something I'm overlooking? Or is this section just stating the obvious?
  - Should we be using "releases"? If so, how?
  - Do we envision deploying (merging + putting code in prod) less or more in an agile world?
  - Should we put customer notes in the repo?

## 4. Ten-Minute Build
  - one-step setup?? (sounds good)
  - automate the build (also sounds good)
  - test suite + code on an env

**Questions:**
 - What should we consider the definition of a build? Is it tests + releasing code? Or something else?
 - Do we want to consider multiple builds? Async builds?

## 5. Continuous Integration
- Big idea: be technologically ready to release even if not functionally
- take the integration token? 
- run a full build
- separate integration machine 
- asynchronous integration - tends to disrupt flow and lead to broken builds

**Questions:**
  - how is this separate integratino machine diff from qa or staging? 
  - How would we envision this in our world with perhaps Docker? 


## 6. Collective Code Ownership
  - I think we do a good job of this for the most part
  - weekly design workshops

## 7. Documentation
  - include non-obvious information
  - API reference docs
  - product documentation
  - tradeoff between written documentation and spoken.
  - when written, gets out of date
  - video of an eloquent team member (lol)
  - keep producing docs until there's a system to take its place

**Questions:**
  - I think it's better to let the code speak for itself, or let tests do the talking. But I could see docs being useful for non-obvious things or API references. What else should we be documenting? Do we need specification docs? I can see it being annoying to have conversations multiple times about the same topic.
