# Chapter 3. Understanding XP

Tight feedback loop. Deploy subsets of the feature weekly so we can hear from the customer how it is performing. - Minimizes the amount of unproven work.

## The XP Lifecycle (1 iteration)

- Planning
  - Business experts help clarify and keep project on track
  - Programers provides estimates and suggestions
  - Most intense during first week of project
  - Work on release plan and touch base daily

- Analysis
  - On site customers figure out the requirements

  > Location 485:
  "They (on-site customer) figure out the general requirements for a story before the programmers estimate it and the detailed requirements before the programmers implement it."

  Would this mean that eng would focus less on writing out the stories? Right now, it feels like we get mocks and then pull the stories out of the mocks and a kick off meeting.

- Design and coding
  - Programmers program using test driven development
  - Programmers pair program

  > Location 499: "Programmers integrate their code every few hours and ensure that every integration is technically capable of deployment."

  How can we make this happen? I feel like the time to deploy QA->staging->prod takes so long and allowing time for others to review make something like this not very practical...

- Testing
  - Programers write tests
  - Customers review WIP and test code through UI and produce examples that programmers to automate testing for
  - Testers user exploratory testing to look for gaps in the code

- Deployment
  - Team demos weekly to stakeholders
  - Team deploys at the end of every iteration

  Deploying so regularly makes it so that the amount of unproven work is small. This allows for the ability to correct mistakes more immediately.

  >Location 467: "At the end of the week, they deploy their software for internal review. (In some cases, they deploy it to actual customers.)"

  This sounds like something we're not quite doing yet. We have deploys that we run all day and then a QA at the end of a project, but not really a 'weekly deploy'.

## The XP Team

> Location 852:
"At the beginning of each iteration, the team meets for a series of activities: an iteration demo, a retrospective, and iteration planning."

This sounds like the rule: if a project is going to last more than a week, there should be weekly checkins.

### Team Members

- On-Site Customers
  - General tasks:
    - Define software to build
    >Location 877:
    "As a rule of thumb, start with two on-site customers (including the product manager) for every three programmers."
    This seems a bit high? Possible answer on 903 - With fewer customers, they are unable to keep up with the programmers?

  - Roles:
    - The product manager
      - Deciding what needs to get build and balancing user feedback and continuing onto new features
    - Domain experts
      - Helps clarify the 'special rules' of the business domain
    - Interaction designers
      - Helps define product UI by understanding the customer
    - Business analysts
      - Liaison between customer and devs. and helps find missed reqs.
- Programmers (4-10 per team)
  - General tasks:
    - Estimate tasks and suggest quicker alternatives
    - Write code and tests that are shippable at the end of each iteration
    >Location 975: "Programmers spend most of their time pair programming. Using test-driven development, they write tests, implement code, refactor, and incrementally design and architect the application."

    The book talks about sticking rigidly to agile and XP programing to start rather than picking and choosing parts that we want to keep and those that we don't. We just recently talked about moving away from pairing so much, but do we really want to head back towards full time pairing?

    >Location 994: "They assist in customer testing by automating the customers’ examples."

    How would we automate examples? Is this just testing as we do it now? Or, because the customer only sees the front end, would this be more JS testing?

    Question: Agile seems to ask for a lot of testing. Right now, testing feels like one of the deploy bottlenecks.
  -Roles:
    - Designers and architects
    - Technical specialists
- Testers
  >Question: Is this a different team than the programmers? How can they run ahead of the team creating tests? This seems like there might be some real difficulty writing tests without really knowing where the code is going? (what objects/services to test...).

  - General tasks:
    - Write tests ahead of programmers
    - Exploratory testing to find gaps in code
- Coaches
  - General tasks:
    - Enable team to succeed
  - Roles:
    - Programing coach
      - Senior dev that can help when needed
    - Project manager
      - Making sure things run smoothly and interfacing with upper management
- Other team roles:
  - Stakeholders
    - Those affected by the project (users, managers, executives)
  - Executive sponsor
    - Person with the $(jQuery)

### Notes on teams

Suggested team sizes: 5 - 12 (20 with some special practices) (location 1094)

Question: All team members should be full time (LocationL 1186). How can we do this with internal customers?

### XP Concepts

- Refactoring
- Technical Debt
- Timeboxing
- The Last Responsible Moment
  - Holding off making decisions when possible so that more information to be accumulated. This is not holding off decisions so long that you lose options
- Stories
- Iterations
  - ~1-3 weeks of shippable work
- Velocity
  - Stories/iteration
- Theory of Constraints
  - Every system has a bottleneck, agile is intentionally building around programmers being the bottleneck. This allows other members to 'scout ahead'
- Mindfulness
  - Pay attention to the process and practices of development

## Start/Stop/Continue

- Keep doing: Daily standup (mentioned at location 851)
- Keep doing: Weekly demos (sounds like weekly iteration demos at location 851) - Do we need to get more 'customers' in this meeting for internal tools?
- Start doing: Get more customer input by doing smaller iterations. It sounds like we are already on our way to doing this, but I know we've sited it as an issues with projects in the past (examples?). The Coffin study on identical teams (location 887 shows the importance of this).
- Start doing: Relocating to sit with different groups? Or inviting key stakeholders to sit with us? (Location 887: If the customer won't move to the team, move the team to the customers.)
- Keep doing: Having dedicated project managers.
- Start doing: TDD. When have we used it on projects? When has it gone well? Why don't we always do it?
Start: Delay decisions until 'the last responsible moment'. This gives more time to accumulate information before making a decision. Very much feels like it works hand in hand with shipping small bits of code, getting feedback, and continuing rather than designing a whole project up front. (Location: 1240)
