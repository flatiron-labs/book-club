Unearthing Concepts

Code is expensive. When is the right time to invest in making your code great? Techniques discussed include using code smells to make code better, flocking rules, making code "Open/Closed" before making changes, and safe refactoring.

"Code is expensive. Writing it costs time or money."
Prompt: How do we balance doing things "right eventually"?
        When is the right time for "right"?

"The conundrum is that once an initial, more prosaic, solution exists, the problem is solved, and the choice of whether to deliver it as is, or to improve upon it at this moment, must be weighed carefully." 
Prompt: Culture of Shame.
        What does it say if our code is "bad"?
        Is there a way to delay "fixing it" until we have to?
        And again, when is that?

New requirements to drive change
"A new requirement tells you
Specifically: What needs to change.
Generally: Raises the standards for the code you're working on.

But generally it’s best to clarify requirements, and then write
the minimum necessary code."
Prompt: Has this burned anyone?
        What does that mean about our communications with stakeholders?
        When we are working on a change, is it worth it to hold of on refactoring today if we "know" it's going to be rewritten in the future?

Open/Closed
"Code is open to a new requirement when you can meet that new requirement without changing existing code.
Prompt: This sounds like Black magic.
        Does anyone have an example of open closed code in our codebase?

...  you should not conflate the process of moving code around, of refactoring, with the act of adding new features"


Code Smells
Note: Great talk. https://www.youtube.com/watch?v=PJjHfa5yxlU
      Code Smells: https://sourcemaking.com/refactoring
      Might be fun to do a code smell hunt in ironboard/phoeyonce

Something fishy
...make a list of the things you dislike about the code.
Definition: "Refactoring is the process of changing a software system in such a way that it does not alter the external behavior of the code yet improves its internal structure."
Change arrangement not behavior

Testing Pain during refactoring
Tests that make assertions about how things are done, rather than what actually happens, are the prime contributors to this predicament. For example, a test that makes assertions about how a method is implemented will obviously break if you change that method’s implementation, even if its output is unchanged

Flocking Rules
Steven note: Assumes shameless green. Warning you may have to make a mess first!
1. Select the things that are most alike.
2. Find the smallest difference between them.
3. Make the simplest change that will remove that difference.
Changes to code can be subdivided into four distinct steps:
1. parse the new code
2. parse and execute it
3. parse, execute and use its result
4. delete unused code

"DRYing out sameness has some value, but DRYing out difference has more."
"You don’t have to identify the underlying abstractions in advance of refactoring. If you merely write the code dictated by the rules, the abstractions will follow."

"The habit of believing that you understand the abstraction, and of jumping to an invented solution, is deeply ingrained. Programmers study a problem, decide on a solution, and then implement it.  Solutions are crafted by intention."
Prompt: Thoughts?

Code excercise
"If an underlying verse abstraction exists, then _this small difference between verse 2 and verses 3-99 must represent a smaller abstraction within that larger one_."


"First, the new requirement. Recall that the impetus for this refactoring was the need to say "six-pack" instead of "bottle/bottles" when there are 6 bottles. The string "six-pack" is one more concrete example of the underlying abstraction. This suggests that if you name the method "bottle," you will regret this decision in short order."

"The general rule is that the name of a thing _should be one level of abstraction higher than the thing itself_. The strings "bottle/bottles/six-pack" are instances of some category, and the task is to name that category using language of the domain."

"The name you choose will be the name you use in conversations with your customers. Naming things after domain concepts improves communication between you and the folks who pay the bills. Only good can come of this."

"When you’re struggling to find a good name but have only a few concrete instances to guide you, it can be illuminating to imagine other things that would also be in the same category." *Steven Pro-tip*

"Real world problems are big. Real code has bugs. Real tests are often tightly coupled to current implementations. If you simultaneously change many things and something breaks, you’re forced to understand everything in order to fix anything. You could end up chasing after red, with increasing desperation, before eventually discarding all of the changes and beginning anew."

"Making a slew of simultaneous changes is not refactoring—it’s rehacktoring."

"In his book Refactoring to Patterns, Joshua Kerievsky talks about "Gradual Cutover Refactoring," a strategy for keeping the code in a releasable state by gradually switching over a small number of pieces at a time."

"The lengthy description above may have led you to fear that working in this fashion would be unbearably slow. Take another look. As you can see, there’s not much code, and with practice, writing it becomes very fast. The small amount of time lost to making incremental changes is more than recouped by avoiding lengthy and frustrating debugging sessions. This style of coding is not only fast, it’s also stress-free."
