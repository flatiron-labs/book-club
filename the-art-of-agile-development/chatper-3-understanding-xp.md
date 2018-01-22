# Chatper 3. Understanding XP

Product manager: Deciding what needs to get build and balancing user feedback and continuing onto new features
Project Manager: Making sure things run smoothly and interfacing with upper management.

Tight feedback loop. Deploy subsets of the feature weekly so we can hear from the customer how it is performing. - Minimizes the amount of unproven work.

Question: Week long iterations - would that mean that we're aiming to do more deploys on Fridays?

## How it works

### Planning

Business experts help clarify and keep project on track
Programers provides estimates and suggestions
Most intense during first week of project
Work on release plan and touch base daily

### Analysis
Location 485:
"They (on-site customer) figure out the general requirements for a story before the programmers estimate it and the detailed requirements before the programmers implement it."
Would this mean that eng would focus less on writing out the stories? Right now, it feels like we get mocks and then pull the stories out of the mocks and a kick off meeting.

Location 495:
"They figure out the general requirements for a story before the programmers estimate it and the detailed requirements before the programmers implement it."

This same location also talks about integrating code every few hours. How can we make this happen? I feel like the time to deploy QA->staging->prod takes so long and allowing time for others to review make something like this not very practical...

Testers using exploratory testing... what is exploratory testing?

Deploying so regularly makes it so that the amount of unproven work is small. This allows for the ability to correct mistakes more immediately.

Location 467:
"At the end of the week, they deploy their software for internal review. (In some cases, they deploy it to actual customers.)"
This sounds like something we're not quite doing yet. We have deploys that we run all day and then a QA at the end of a project, but not really a 'weekly deploy'.

Location 852:
"At the beginning of each iteration, the team meets for a series of activities: an iteration demo, a retrospective, and iteration planning."
This sounds like the rule: if a project is going to last more than a week, there should be weekly checkins.

Location 877:
"As a rule of thumb, start with two on-site customers (including the product manager) for every three programmers."
This seems a bit high?
Answered on 903 - With fewer customers, they are unable to keep up with the programmers?

Keep doing: Daily standup (mentioned at location 851)
Keep doing: Weekly demos (sounds like weekly iteration demos at location 851) - Do we need to get more 'customers' in this meeting for internal tools?
Start doing: Get more customer input. It sounds like we are already on our way to doing this, but I know we've sited it as an issues with projects in the past (examples?). The Coffin study on identical teams (location 887 shows the importance of this).
Start doing: Relocating to sit with different groups? Or inviting key stakeholders to sit with us? (Location 887: If the customer won't move to the team, move the team to the customers.)

Keep doing: Having dedicated project managers.

Domain experts: How does this role fit in with our work/features? Since our team is small, are we relying on the product manager to be the domain expert? (ref location 939)

Start doing: Business Analysis? (location 975)

Location 975: Programmers spend most of their time pair programming. Using test-driven development, they write tests, implement code, refactor, and incrementally design and architect the application.
The book talks about sticking rigidly to agile and XP programing to start rather than picking and choosing parts that we want to keep and those that we don't. We just recently talked about moving away from pairing so much, but do we really want to head back towards full time pairing?
Start doing: TDD. When have we used it on projects? When has it gone well? Why don't we always do it?

Location 994: They assist in customer testing by automating the customers’ examples.
How would we automate examples? Is this just testing as we do it now? Or, because the customer only sees the front end, would this be more JS testing?

Testers (location 1013)- Is this a different team than the programmers? How can they run ahead of the team creating tests? This seems like there might be some real difficulty writing tests without really knowing where the code is going? (what objects/services to test...).

Question: Agile seems to ask for a lot of testing. Right now, testing feels like one of the deploy bottlenecks.

Suggested team sizes: 5 - 12 (20 with some special practices) (location 1094)

Full-Time members - All team members should be full time (LocationL 1186). How can we do this with internal customers?

Start: Delay decisions until 'the last responsible moment'. This gives more time to accumulate information before making a decision. Very much feels like it works hand in hand with shipping small bits of code, getting feedback, and continuing rather than designing a whole project up front. (Location: 1240)
