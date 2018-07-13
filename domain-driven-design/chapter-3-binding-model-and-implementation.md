# Chapter 3 Binding Model and Implementation

Problem/Example: A giant pre-mapped model ended up being very similar to a hacked together app that was built ad-hoc. In both cases it was hard to understand what the code did by looking at the model.

## Model Driven Design

Definition:
> Tightly relating the code to an underlying model gives the code meaning and makes the model relevant. (pg 28)

Risk: Models and code deviate and things become difficult to understand.

Question: What is an example of an 'analysis model'. Not sure I really understand this section.
Answer: A model that is put together ahead before the actual model just to understand the business domain. 

> If the design, or some central part of it, does not map to the domain model, that model is of little value, and the correctness of the software is suspect. At the same time, complex mappings between models and design functions are difficult to understand and, in practice, impossible to maintain as the design changes. A deadly divide opens between analysis and design so that insight gained in each of those activities does not feed into the other. (pg 29)

The chosen model must fit all purposes (design and analysis)

> The code becomes an expression of the model, so a change to the code may be a change to the model. (pg 29)

## Model Paradigms and Tool Support

OO Design is a great tool because it is itself a type of modeling. It can really strengthens the connection between the code and the model. It's harder to with a procedural language like C

Question: I find it a bit hard to think about OO design vs. non-OO design, perhaps because I am most familiar with Ruby. Did others have this problem? Or perhaps a better way of understanding this?

Model driven design is useful for testing as you can now use unit tests. The only way to test scripts is end to end.

## Letting the Bones Show: Why Models Matter to Users

You run into problems when the user is interacting with different models than the program is built on (example: bookmarks being stored as files and now having the same constraints as file names do). Revealing the model to the user helps mitigate this.

Question: What are some examples of where we do this in Learn? and some example of where we don't?

## Hands-On Modelers

It's important to have the modelers also help write code so they can help convey the intent of the design. Modelers will also quickly lose feel for the constraints of the implementation if they're not coding.

Question: Did others find this section applicable to our team? We don't really have a concept of modelers and coders as different people. We are starting to have concepts to tech advisors, is this something we need to watch out for?
