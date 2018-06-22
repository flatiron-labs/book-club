# Domain Driven Design Chapter 1 and Domain Modeling Made Functional Chapter 1

## Why DDD?
Both books covered how getting a better understanding of the domain can help you not only understand the proposed solution, but also be more valuable to the team since you can help identify where the rules that people just "get" are.

DMMF
>A Developer's job is to solve a problem through software, and coding is just one aspect of software development.
What are out thoughts on this? Is it true? Is it a team value?

>Domain Driven design is not appropriate for all software development... However it is particularly useful for business and enterprise software, where developers have to collaborate with other nontechnical teams...

## Shared Models

>It's the developers understanding, not the domain experts' understanding, that gets released to production.

**definition**
Development Team: Not just developers, but also UX and UI Designers, testers and so on.

>Connections to Agile: The development team regularly delivers something to the domain expert, who can quickly correct any misunderstandings for the next iteration.

>The developer acts as a translator, translating the domain expert's mental model into code.
XP is more about process. This is more about communication. Sort of...

> The code is designed to reflect the shared mental model directly
What's hard about this? Checklists come to mind.

## Understanding the Domain Through Business Events
> The value of the business is created in this process of transformation, so it is critically important to understand how these transformations work and how they relate to each other.

> Domain Events are teh starting point for almost all of the business processes we want to model
> Domain Events are always written in the past tense-- something happened-- because it's a fact that can't be changed.

## EventStorming
Love this idea
> The attendees should include not just developers and domain experts but all the other stakeholders who have an interest in the success of the project... "Anyone who has questions and anyone who has answers"

> During the workshop, people write down business events on the sticky notes and post them on the wall. Other people may respond by posting notes summarizing the business workflows that are triggered by these events. These workflows, in turn, often lead to other business events being created. In addition, the notes can often be organized into a timeline, which may well trigger further discussion in the group. 

**Benefits**
*A shared model of the business*
> As well as revealing the events, a key benefit of Event Storming is that the participants develop a shared understanding of the business, because everyone is seeing the same thing on the big wall. 
No us vs them

** Getting clarification on questions**
> If the question doesn’t have a clear answer, then the question itself should be posted on the wall as a trigger for further discussion. 
> It’s common for the requirements to be fuzzy at the beginning of a project, so documenting the questions and debate in this visible way makes it clear more work needs to be done, and it discourages starting the development process prematurely.
Now is not the time to start thinking about queues vs databases.

**Surfacing reporting requirements**
There's always reporting. These should be brought up.

## Partitioning The Domain into Subdomains
**definition**
Domain: In the DDD World, a domain is an area of coherent knowledge.

## Creating a solution using Bounded Contexts
>Understanding the problem doesn’t mean that building a solution is easy. The solution can’t possibly represent all the information in the original domain, nor would we want it to. We should only capture the information that is relevant to solving a particular problem. Everything else is irrelevant.

> it’s important that each bounded context have a clear responsibility, because when we come to implement the model, a bounded context will correspond exactly to some kind of software component.
** Getting Contexts Right**
> Listen to the domain experts. If they all share the same language and focus on the same issues, they are probably working in the same subdomain (which maps to a bounded context).
> Pay attention to the existing team and department boundaries.
> Don’t forget the “bounded” part of a bounded context. Watch out for scope creep when setting boundaries.


**definition**
Generic Domains: Domains not specific to your business

## Creating Ubiquitous language
> That means that things in our design must represent real things in the domain expert’s mental model. That is, if the domain expert calls something an “order,” then we should have something called an Order in the code that corresponds to it and that behaves the same way.

** Ubiquitous Language is fluid **
Don't expect it to be static.
> Each context will have a “dialect” of the Ubiquitous Language, and the same word can mean different things in different dialects.
> All the attendees used the word “order” when describing events. But we might well find that the shipping department’s definition of “order” is subtly different definition than the billing department’s definition.

