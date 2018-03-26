## Chapter 9 - Developing (Part 2)

### Simple Design (Programmers)

*Allows design to change to support feature requests*

- Don't anticipate changes when writing code, just write the simplest code needed to solve the problem
  - "Unintuitively, this results in designs that are ready for any change, anticipated or not." - pg. 317
  - DISCUSSION: Even though I try to do this, I always feel like conversations such as "Well, we are going to be doing X soon after this..." seem to crop up pretty frequently. Am I taking this _too_ literally? How do we feel we do as a team on this?

- Once and only once
  - Should we be following this instead of rule of three? (refactor code into a single place if it's used in _three_ places)

- Limiting published interfaces.
  - Have as few interfaces as possible that are used by external teams
  - Not sure this is an issue right now (I don't think we have code used outside our team), but perhaps something we may need to start thinking about with 2U?

- Fail Fast
  - I think we do this well with guard clauses? `return false unless current_user`...?

### Incremental Design and Architecture (Programmers)

*Programmers can work on features in parallel with technical infrastructure. We deliver stories every week without compromising design quality.*

- Only build for the immediate problem, do not try and generalize before it's needed.

- DISCUSSION: Incremental Design for things like architecture. The book seems to imply refactoring a small portion of the code base with the architecture and trying it out? (pg 328) This seems pretty steep.

- Risk-Driven Architecture
  - You can _think_ about future problems and code towards them as long as you don't implement future stories in the process.(pg 329) This feels like it goes against Simple Design?

### Spike Solutions (programmers)

Performing small, isolated experiments when we need more information.

- Spikes are usually so small, they are done inline with your work. Larger spikes that you know are blocking for a story though should have a story of their own.

- Don't copy spike solutions into the code base. Re-write the code needed using TDD

### Performance Optimization (programmers, testers)

Hard data to drive optimization

- Programing is too complex to really understand bottlenecks before you see them in practice. Over optimizing can even make things _worse_.

- Performance testing is a good use case for end-to-end testing.

- Stories around optimization testing need concrete goals (e.g.: Throughput, Latency, Responsiveness)

- DISCUSSION: If we do not try and optimize anywhere without measuring, can't we run the risk of a death by a thousand paper cuts type situation?

### Exploratory Testing (Testers)

IDs gaps in team process

- Test don't just hunt for bugs, they look at the code with a fresh set of eyes and find gaps

- Exploratory testing can be great for finding cross-story gaps
  - Can be manual or automated

- Tools:
  - Charters - Having a map of where you're going to stay focused / the testing equivalent to a story.
  - Observations - Looking at things as a human such that you can notice more than an automated test
  - Note taking - Ensures that you know how you got to where you are and what you did to get there. (Maybe add a screen recorder to this tool?)
  - Heuristics - frequent testing patterns that you may want to try applying to different situations. (Boundary testing, None Some All, Goldilocks, Position, Count, CRUD, Command Injection...)
