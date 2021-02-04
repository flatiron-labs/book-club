# Part 3: Building

## [Chapter 10: Hand Over Responsibility](https://basecamp.com/shapeup/3.1-chapter-10)

### Assign projects, not tasks

* There is not "taskmaster" who divvies up the project into pieces because we want project to stay whole throughout the entire process so people do not lose sight of the bigger picture
* Don't want to fall into trap where everyone is just worried about their small piece and no one feels responsible for how everything fits together
* Team defines their own tasks and workflow autonomously

### Done means deployed

* There should be deployed work at end of cycle. This includes all testing and QA

### Getting oriented

* Following cycle kick-off, first few days of cycle are pretty quiet because everyone is trying to figure out how existing system works and thinking about the best starting points
* Exploratory period that is usually no longer than 3 days

### Imagined vs discovered tasks

* Team comes up with own tasks
* Imagined tasks - tasks we think we need to do at the start of a project 
* Discovered tasks - tasks we discover we need to do in the course of doing real work that we didn't know in advance, most tasks will be this variety
*  The way to really figure out what needs to be done is to start doing real work

## [Chapter 11: Get One Piece Done](https://basecamp.com/shapeup/3.2-chapter-11)

* Good idea to aim to get something tangible and demoable done early

### Integrate one slice

* Typically want to do something that requires integrating vertically on one small piece of the project instead of chipping away at the horizontal layers early on
* If you start with front end or back end, nothing will work until full integration occurs
* By picking off vertical slice first, team has something tangible that they’ve proven to work (or not work and reconsider)
* Seems to allow for flexibility if changes to approach need to be made

### Affordances before pixel-perfect screens

* When starting implementation, programmers don't need pixel-perfect screens, all they need are endpoints (input elements, buttons, places where stored data should appear)
* This allows us to ask important questions like Does it make sense? Is it understandable? Does it do what we want? as early as possible

### Program just enough for the next step

* Early back-end work can be strategically patchy
* Not everything needs to be in place and functional in order for decisions to be made
* The point is to create a back-and-forth between design and programming on the same piece of the product to better understand how project is coming along and what to do next

### Start in the middle

Three criteria to think about when choosing what to build first
1. It should be core. Something that is more central and important to prove out early in the cycle
2. It should be small. The point is to finish something meaningful in a few days and build momentum—to have something real to click on that shows the team is on the right track
3. It should be novel. If two parts of the project are both core and small, prefer the thing that you’ve never done before so the team learns something new and uncertainty is eliminated

## [Chapter 12: Map the Scopes](https://basecamp.com/shapeup/3.3-chapter-12)

### Organize by structure, not by person

* Builds off of previous vertical slicing concept
* Should base project tracking off of structure of the project - the things that can be worked on and finished independently of each other
* Need to figure out where the interdependencies are, how things are connected, and what can be sliced apart
* Each slice that can be worked on and finished independently is called a "scope"

### The scope map

* All the sliced scopes inside the larger scope of the project
* Scopes reflect the meaningful parts of the problem that can be completed independently and in a short period of time (few days or less). Are usually bigger than tasks
* Scopes are the language of the project

### Discovering scopes

* Scopes develop as team digs into the work. Becomes more accurate around week 1/2 of cycle
* Scopes arise from interdependencies. The way parts depend on each other determines when you can say a given piece of the work is “done.”

### How to know if the scopes are right

Three signs that indicate when the scopes are right
1. You feel like you can see the whole project and nothing important that worries you is hidden down in the details.
2. Conversations about the project become more flowing because the scopes give you the right language.
3. When new tasks come up, you know where to put them. The scopes act like buckets that you can easily lob new tasks into.

Three signs that indicate the scopes should be redrawn
1. It’s hard to say how “done” a scope is. This often happens when the tasks inside the scope are unrelated. If the problems inside the scope are unrelated, finishing one doesn’t get you closer to finishing the other.
2. The name isn’t unique to the project. This suggests you aren’t integrating enough, so you’ll never get to mark a scope “done” independent of the rest.
3. It’s too big to finish soon. If a scope gets too big, with too many tasks, it becomes like its own project with all the faults of a long master to-do list. Better to break it up into pieces that can be solved in less time, so there are victories along the way and boundaries between the problems to solve.

### Different kinds of tasks and scopes

* Layer cake: front end and back end layered on top of each other 
* Icebergs: significantly more front end or back end work. Helps to question why the larger piece is significantly more complicated and whether it can be simplified
* Chowder: loose tasks that don't fit anywhere. If this gets to longer than 3-5 tasks, then there's probably a scope missing somewhere
* Nice-to-haves: good idea to track so can sort by must-haves and nice-to-haves

## [Chapter 13: Show Progress](https://basecamp.com/shapeup/3.4-chapter-13)

* Managers would rather be able to just see status without having to ask explicitly for it
* To dos aren't great for this

### The tasks that aren’t there

* To dos could have tasks that still need to be added and just haven't been defined yet
* To dos are in a state of flux for a lot of development. QA could find more tasks that need to be added even late in the cycle

### Estimates don’t show uncertainty

* Estimates have different meaning depending on nature of work being estimated
* Can't accurately estimate unknown unknowns

### Work is like a hill

* Want to focus instead on what's unknown and what's solved
* "Hill Charts"
* Uphill phase is when you're figuring out what the approach is and what is going to be done
* Top of the hill is when you feel like you know what you need to do
* Downhill phase is execution

### Scopes on the hill

* Can combine hill with concept of scopes
* Scopes represented by color and move along hill depending on where they are in the uphill/downhill phases ([Example](https://basecamp.com/assets/books/shapeup/3.4/scopes_on_the_hill-592ba06433e0fbc0e45c6344efdcb44e7d2c495b8d0f0d6048e2b8aa030acb88.png))
* Allows managers to get an at-a-glance view of individua statuses of scopes and overall status of project
* If dot for scope doesn't move, likely means someone is stuck and conversation can be facilitated
* Sometimes dot not moving just means scope is too large and needs to be refactored. Once broken down, team can show more progress more frequently

### Build your way uphill

* Can think of first third of uphill as "I've thought about this"
* Second third as "I've validated my approach"
* Final third as "I’m far enough with what I’ve built that I don’t believe there are other unknowns"

### Solve in the right sequence 

* Can use hill chart to sequence scopes
* Typically want to push work with most unknowns up the hill first, once it's at the top can leave it there and start getting some other critical scopes up the hill before going back to complete

## [Chapter 14: Decide When to Stop](https://basecamp.com/shapeup/3.5-chapter-14)

How do we make the call to say what we have is good enough and move on?

### Compare to baseline

* Don't compare to the ideal. Compare to baseline - the current reality for customers

### Scope cutting/hammering

* Since there is a 6-week circuit breaker, if work doesn't get down the project doesn't ship
* When people want to shift scope, need to question if it can actually fit in time frame and make trades offs if necessary
* Teams should have tools, authority, and responsibility to constantly cut down scope
* Cutting scope is decision making that makes the product better at some things instead of others which differentiates the product
* Questions to ask when scope hammering
  * Is this a “must-have” for the new feature?
  * Could we ship without this?
  * What happens if we don’t do this?
  * Is this a new problem or a pre-existing one that customers already live with?
  * How likely is this case or condition to occur?
  * When this case occurs, which customers see it? Is it core—used by everyone—or more of an edge case?
  * What’s the actual impact of this case or condition in the event it does happen?
  * When something doesn’t work well for a particular use case, how aligned is that use case with our intended audience?

### QA

* Focuses on edge cases
* QA generates discovered tasks that are all nice-to-haves by default since must-haves should have all been done when scope was completed
* Can collect QA issues on a separate list and if any of them become must-haves, can move them into specific scope

### Code Review

* Basecamp doesn't use code review as a formal checkpoint and team can ship without it
* They view it as more of a teaching opportunity

### When to extend a project

* Extend a project instead of pull circuit breaker
** outstanding tasks must be true must-haves that withstood every attempt to scope hammer them
** outstanding work must be all downhill. No unsolved problems; no open questions
* If there's uphill work left at the end of a cycle indicates oversight in shaping or hole in concept

## [Chapter 15: Move On](https://basecamp.com/shapeup/3.6-chapter-15)

* Take some time after shipping to let things settle before considering feedback and requests
* Any requests and bugs can become a new bet and need to be shaped so you start process over again
