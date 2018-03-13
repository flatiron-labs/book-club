# Chapter 8: Planning (part 2)

## Iteration Planning

### Takeaways:

* We stop at predetermined, unchangeable time intervals and compare reality to plan.
* Iterations are the heartbeat of an XP project.
* Although the iteration timebox doesn’t prevent problems, it reveals them, which gives you the opportunity to correct the situation.
* Iteration schedule:
  - Demonstrate previous iteration (up to half an hour)
  - Hold retrospective on previous iteration (one hour) 
  - Plan iteration (half an hour to four hours)
    * Start by measuring the velocity of the previous iteration.
    * With your velocity in hand, you can select the stories to work on this iteration.
    * Because the iteration planning meeting takes stories from the front of the release plan, you should have already estimated and prioritized those stories.
    * After you have chosen the stories for the iteration, everybody but the programmers can leave the meeting, although anybody is welcome to stay if she likes.
    * At this point, the real work of iteration planning begins. Start by breaking down the stories into engineering tasks.
    * Brainstorming tasks is a design activity. If everybody has the same ideas about how to develop the software, it should go fairly quickly. If not, it’s a great opportunity for discussion before coding begins.
    * Finish brainstorming before you start estimating.
    * Call out the estimates as you finish them. If you hear somebody call out an estimate you disagree with, stop to discuss it and come to consensus.
    * Estimate the tasks in ideal hours.
    * As a final check, add up the estimates and compare them to the total task estimates from your previous iteration.
    * Discuss the situation with your on-site customers...adjust the plan until the team is ready to commit to delivering its stories.
  - Commit to delivering stories (five minutes) Develop stories (remainder of iteration)
    * Ask each person, in turn, if he can commit to doing so. Wait for a verbal “yes.”
  - Prepare release (less than 10 minutes)
    * At the end of the iteration, release your completed software to stakeholders. With a good 10-minute build, this shouldn’t require any more than a button press and a few minutes’ wait.
* When things go wrong
  - When you discover a problem that threatens your iteration commitment, first see if there’s any way you can change your plan so that you still meet your commitments.
  - Sometimes the problem will be too big to absorb. In this case, you’ll usually need to reduce the scope of the iteration.
  - Under no circumstances, however, should you change the iteration deadline.
  - After changing the plan, the customers should reestablish trust with stakeholders by explaining what happened, why, and what the team is doing to prevent this sort of problem in the future.
* Emergency requests
  - You can change the iteration schedule under the condition that you take out as much work as you add.
  - an emergency in every iteration means that something is wrong.
  - In some cases, however, the team has a legitimate need to provide ongoing support for ad hoc requests. If this is true for your team, sacrifice a programmer to be the batman.
  - Rotate a new programmer into the batman role every iteration to prevent burn-out.
* When you use iterations well, your team has a consistent, predictable velocity.
* Never artificially inflate your velocity. Similarly, don’t use commitment as a club. Never force team members to commit to a plan they don’t agree with.
* Energized work is also important. Without it, the team will have trouble maintaining equilibrium and a stable velocity.
* Iteration length:
  - Many teams prefer two-week iterations.
  - shorter iterations means more rapid improvement for a team new to XP.
  - One-week iterations also make decisions easier by reducing schedule risk.
  - one-week iterations put more pressure on the team.
  - Velocity is less stable in one-week iterations
  - Two-week iterations are a little less stressful and lead to a more stable velocity.

### Talking Points/Questions:

* What aspects of iteration planning seem like they would be a good fit for Labs?
* What problems could we solve with iteration planning?
* What new problems could we have with iteration planning?

## Slack

### Takeaways:

* This allows us to compensate for randomness and keep a steady velocity
* A better approach is to schedule useful, important work that isn’t time-critical — work you can set aside in case of an emergency. Paying down technical debt fits the bill perfectly.
* Rather than doing the bare minimum necessary to keep your head above water, be generous in refactoring and cleaning up technical debt in existing code.
* A good rule of thumb is to spend 10 percent of the iteration on technical debt. (Perform big refactorings incrementally.)
* As you fix technical debt, focus on fixes that make your current work easier. Don't focus on unrelated stuff.
* Dedicated research time is an excellent way to encourage learning and add additional slack into your iterations.
* The continuous drumbeat of iteration deadlines is great for reducing risk and motivating the team to excel, but it can lead to tunnel vision. Dedicated research time gives programmers a chance to widen their ranges, which often leads to insights about how to develop more effectively.
* Be careful not to overuse overtime. Overuse will sap team members’ ability to do good work. You can use it to clean up after small problems, but each programmer should only contribute an hour or so per day, and only voluntarily.
* In my experience, there are two big sources of randomness on XP teams: customer unavailability and technical debt.
* The danger of thinking of these tasks as slack is thinking they aren’t important. They’re actually vital, and a team that doesn’t perform these tasks will slow down over time.

### Talking Points/Questions:

* Can companies that don't have slack not meet their commitments because they are pushing their limits?
* What would "slack" look like for labs? Which practices seem good for us? What do we already do?

## Stories

### Takeaways:

* Stories are for planning. They’re simple one- or two-line descriptions of work the team should produce.
* Story characteristics:
  1. Stories represent customer value and are written in the customers’ terminology. (The best stories are actually written by customers.) They describe an end-result that the customer values, not implementation details.
  2. Stories have clear completion criteria. Customers can describe an objective test that would allow programmers to tell when they’ve successfully implemented the story.
* physical cards have one feature that no conglomeration of pixels has: they’re tactile.
* Stories need to be customer-centric.
* include any technical considerations in the estimate for each story.
* Sometimes programmers won’t be able to estimate a story because they don’t know enough about the technology required to implement the story. In this case, create a story to research that technology.
* When you use stories well, the on-site customers understand all the work they approve and schedule. You work on small, manageable, and independent pieces and can deliver complete features frequently. The project always represents the best possible value to the customer at any point in time.

### Talking Points/Questions:

* How do we use stories now? Pros / cons?

## Estimating

### Takeaways:

* Are good estimates possible? Of course! You just need to focus on your strengths.
* One reason estimating is so difficult is that programmers can rarely predict how they will spend their time.
* Part of the secret to making good estimates is to predict the effort, not the calendar time, that a project will take. Make your estimates in terms of ideal engineering days (often called story points), which are the number of days a task would take if you focused on it entirely and experienced no interruptions.
* In a mature XP team, velocity is stable enough to predict schedules with a high degree of accuracy
* Velocity relies upon a strict iteration timebox. To make velocity work, never count stories that aren’t “done done” at the end of the iteration. Never allow the iteration deadline to slip, not even by a few hours.
* You may be tempted to cheat a bit and work longer hours, or to slip the iteration deadline, in order to finish your stories and make your velocity a little higher. Don’t do that! Artificially raising velocity sabotages the equilibrium of the feedback cycle.
* Velocity tends to be unstable at the beginning of a project. Give it three or four iterations to stabilize. After that point, you should achieve the same velocity every iteration, unless there’s a holiday during the iteration.
* All the programmers should participate in estimating. At least one customer should be present to answer questions.
* It’s almost a law of physics: customers and stakeholders are invariably disappointed with the amount of features their teams can
provide. Sometimes they express that disappointment out loud. The best way to deal with this is to ignore the tone and treat the comments as straightforward requests for information.
* This approach also requires trust: developers need to believe they can give accurate estimates without being attacked, and customers and stakeholders need to believe the developers are providing honest estimates.

### Talking Points/Questions:

* What are the greatest obstacles for Labs to make good estimates right now?
* How much better would our lives be if we could estimate perfectly?
