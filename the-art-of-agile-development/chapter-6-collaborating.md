# Chapter 6: Collaborating

Better information sharing => more effective team => higher quality software.

Better information sharing => more informed managers + customers => better feedback + schedule management.

#### Chapter summary:

> _Trust_ is essential for the team to thrive.  
> _Sitting together_ leads to fast, accurate communication.  
> _Real customer involvement_ helps the team understand what to build.  
> _Ubiquitous language_ helps team members understand each other.  
> _Stand-up meetings_ keep team members informed.  
> Coding standards provide a template for seamlessly joining the team’s work together.  
> _Iteration demos_ keep the team’s efforts aligned with stakeholder goals.  
> _Reporting_ helps reassure the organization that the team is working well.  

Goal: remove communication bottlenecks.

#### Breakout session ("mini-etude")

Recommendation: Do this exercise for 30min every day

##### Materials:
- white, red, yellow, green index cards
- empty table or whiteboard
- writing implements for everyone

##### Step 1:
- Form pairs
- Work with a new partner every day

##### Step 2 (10 minutes)
- Discuss info you need to do your job
- Discuss info people need from you to do their job
- Think of a specific example
  - How much time did it take to get/provide the needed info?
  - How much time does that typically take?
    - < 10 minutes => green card
    - < 1 day => yellow card
    - >= 1 day => red card
  - Write down type of info, groups involved, time required on card

##### Step 3:
- Discuss ways to reduce time needed
- Pick one example and write it on white card

##### Step 4:
- Discuss all cards as a team


## Trust

> We work together effectively and **without fear.**

Group dynamics: “Forming, Storming, Norming, and Performing”

How does a team become productive?  
- Joint responsibility
- Teammates are "us", not "them"
- Happy to help each other

Taking time to help others is valuable and valued:

> You need to trust that taking time to help others won’t make you look unproductive.

Mutual respect:

> You need to trust that you’ll be treated with respect when you ask for help **or disagree with someone**.


Strategies:

#### Team Strategy 1: Customer-Programmer Empathy

Lack of trust stems from lack of empathy.

Solutions?  
- Sit together.
- Retrospectives

#### Team Strategy 2: Programmer-Tester Empathy

[KT Note] This section was mostly just advice on manners.

Respect on both sides: respect testers coding skills, don't just try to shoot down programmers work.

Thank testers for finding bugs.

Don't gloat when you find a bug.


#### Team Strategy 3: Eat Together

One free meal per week? Sounds great.



#### Team Strategy 4: Team Continuity

Keep productive teams together.

Keep people together across multiple projects


#### Impressions

Depressing anecdote about an effective XP team getting let go.

> When [management] looked in on the XP team, they saw people talking, laughing, and going home at five with nothing but rough sketches and charts on the whiteboards.

Lesson:

> No matter how effective you are at meeting your technical commitments, you’re in trouble without the good will of your stakeholders.

#### Organizational Strategy #1: Show Some Hustle

Translation: look busy?

> Energized work, an informative workspace, appropriate reporting, and iteration demos all help convey this feeling of productivity.


#### Organizational Strategy #2: Deliver on Commitments

Customers often don't know what good software development looks like. They don't know how to evaluate your process, so we need to show them something they can understand: results.

#### Organizational Strategy #3: Manage Problems

> The bigger the problem, the sooner you should disclose it.

- Limit exposure to problems
- Work on hardest, most unclear tasks early (so you have more time to solve them)
- When you hit a problem, let the whole team know (don't hide it)
- Budget more time to solve problem
  - Reduce (unneccessary) code cleanup
  - Postpone non-essential meetings
  - Cancel research time
- Let the stakeholders know (defer to product manager on timing)

> Reliance on overtime indicates a systemic problem.


#### Organizational Strategy #4: Respect Customer Goals

- Customers feel weird working with programmers, so programmers need to make the extra effort
- Instead of shutting down customer goals, put energy into finding creative alternatives for meeting them

Example of taking 10 minutes to turn a customer request into a story... good suggestion? Has anyone done this? Was it helpful?

#### Organizational Strategy #5: Promote the Team

Be visible to the rest of the company.  
- Brown bag lunches
- Board with pictures and assignments on it
- Open demos

#### Organizational Strategy #6: Be Honest

Again, a lesson in good behavior.

> Don't give stakeholders the impression you've don't more than you actually have

- Don't gloss over problems during demo
- Don't take credit for story that's not actually done
- Don't push deadline back just to finish everything (?)

#### Questions

Give your team time to get through the "stormy" stage

Overtime can solve small problems; don't become reliant on it

Be careful about joking (might be mis-read)

#### Contraindications

Compensation based on individual performance interferes with good team dynamic.


## Sit Together

**Seems like biggest challenge for our team,** especially as we add more distributed teammates.

Cites lots of examples of better performance w/ co-location.

Benefits of "osmotic communication"... seems like how we were all sold on the open office concept.

> Because they’ll be working together, this buzz won’t be too distracting for team members.

^^ Is that actually true for everyone? There's a reason our team all has big noise-cancelling headphones. Book says "worries about distractions and noise... [are] usually a cover for one of the other concerns." Seems a little dismissive.

Further reading that might be helpful for us: “Follow the Sun: Distributed Extreme Programming Development” [Yap] is an interesting experience report describing a single XP team divided into three locations, each eight hours apart.


## Real Customer Involvement

Helpful but not crucial.

#### Personal Development

- Dev team is its own customer, buiding software for its own use
- Often throwaway, might not need full XP team

#### In-House Custom Development

- Organization asks team to build something for org's own use
- Multiple customers: executive + end users
- Easier to involve real customers bc they're your co-workers


#### Outsourced Custom Development

- Harder to recruit on-site customers
- Move your team to customers, not vice versa

#### Vertical Market Software

- Built for an industry, often customized per customer
- Many customers
- Set limits on influence of single customer

#### Horizontal Market Software

- Used across wide range of industries
- Wide audience


## Ubiquitous Language

Reduce the risk of miscommunication.

Conundrum:

> The people who are experts in the problem domain — the domain experts — are rarely qualified to write software.
> The people who are qualified to write software — the programmers — don’t always understand the problem domain.

Backwards advice? When choosing between great programmer with no domain experience vs. poor programmer with lots of domain experience, go with better programmer?

Domain Driven Design:

> Programmers should speak the language of their domain experts, not the other way around.
> ...[reflect] in code how the users of the software think and speak about their work.

Ubiquitous language can change, but you need to maintain group concensus.



## Stand-up Meetings

Status meetings: long, inefficient use of time

Stand-up meetings: short, efficient

Timing:

> If people arrive at different times, early arrivals sometimes just waste time until the stand-up starts.
> You can reduce this problem by moving the stand-up to later in the day, such as just before lunch.

Advice for keeping things short and sweet:  
- Write statement on card beforehand, then read from card.
- Use a timer

Ok to include people from outside the team

!!! PARKING LOT THERAPY?

> People are always late to the stand-up. Can we treat them to parking-lot therapy?
> I’ve been tempted to introduce Mr. Laggard to Mr. Baseball Bat myself.



## Coding Standards

More than just formatting. Agree on more important practices, like never passing null references between objects, when to handle exceptions, etc.

> Two recommended guidelines:
>
> 1. Create the minimal set of standards you can live with.
> 2. Focus on consistency and consensus over perfection.

Use multiple, hour long meetings to hash out standards. Be diplomatic.

Consider leaving hotly contested items out of the standard. You'll probably learn from the lack of standardization, then make a better informed decision later.

If people aren't following the standard, investigate why. Might discover it needs to be changed.


## Iteration Demo

- Keeps the team honest about progress
- Chance to be proud, show off work
- Keep stakeholders informed
- Good opportunity to solicit feedback
- "Full disclosure will raise your credibility"


> Two key questions for your expecutive sponsor:
>
> 1. Is our work to date satisfactory?
> 2. May we continue?

Note: "Inability to demo is a clear danger sign."


## Reporting

#### Progress reports

- Vision statement (created with customer)
- Weekly demo
- Release and iteration plans
- Burn up chart

Note: author uses a webcam to broadcast boards, if neccessary, which came up in conversation last week.


Optional:  
- Roadmap
- Status email

#### Management reports

- Productivity (trick: finding the right metric)
- Throughput
- Defects
- Time usage (logging hours)

Reports to avoid:  
- Lines of code / function points (encourages defects and high costs)
- Number of stories
- Velocity
- Code quality

