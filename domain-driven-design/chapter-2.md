## Chapter 2: Communication and the Use of Language

General Principles

1. A domain model can be the core of a common language for a software project.
2. The model is a set of concepts built up in the heads of people on the project, with terms and relationships that reflect domain insight.
3. These terms and interrelationships provide the semantics of a language that is tailored to the domain while being precise enough for technical development.

** A common language is a crucial cord that weaves the model into development activity and binds it with the code. **


## I. Ubiquitous Language
(aka a versatile, shared team language)

The Players

- Domain experts: jargon of the field
- Developers: descriptive, functional terms

> Across this linguistic divide, the domain experts vaguely describe what they want. Developers, struggling to understand a domain new to them, vaguely understand. A few members of the team manage to become bilingual, but they become bottlenecks of information flow, and their translations are inexact.

** Also, lack of shared language between devs working on different parts of the same domain (i.e. different design concepts and ways of describing the domain) **

### The Act of Translation
On a project without a common language...

- Developers translate for domain experts
- Domain experts translate between developers and other domain experts
- Developers even translate for each other

> Translation muddles model concepts, which leads to destructive refactoring of code. The indirectness of communication conceals the formation of schisms—different team members use terms differently but don't realize it.

### Terminology
- *UBIQUITOUS LANGUAGE:* names of classes and prominent operations
- *LANGUAGE:* terms to discuss rules that have been made explicit in the model

> Persistent use of the UBIQUITOUS LANGUAGE will force the model's weaknesses into the open.

### Commitment is Key

Commiting to an ubiquitous language will...

- Point out **imprecision** or** contradiction** and engage the domain experts in discovering workable alternatives.
- Lead to a model that is **complete** and **comprehensible**, made up of simple elements that combine to express complex ideas.

> Use the model as the backbone of a language. Commit the team to exercising that language relentlessly in all communication within the team and in the code. Use the same language in diagrams, writing, and especially speech.

Applies to all communication types: *CODE*, *DIAGRAMS*, *WRITING*, *SPEECH*

### Terminology Confusion!

STEPS

1. Resolve confusion over terms just the way we come to agree on the meaning of ordinary words in a conversation.
2. If there is a change in the UBIQUITOUS LANGUAGE, change the model accordingly.

Shared Responsibility

- *Domain experts:* should object to terms or structures that are awkward or inadequate to convey domain
- *Developers:* should watch for ambiguity or inconsistency that will trip up design

## II. Example: Working Out a Carrier Router

### Scenario 1: Minimal Abstraction of the Domain

Talking almost exclusively in database tables, very little communication about actual domain

UBIQUITOUS LANGUAGE used: Cargo, Routing Service

### Scenario 2: Domain Model Enriched to Support Discussion
In this dialog, the route spec and itinerary are discussed in specific terms including attributes and procedures

UBIQUITOUS LANGUAGE used: Cargo, Routing Service, Route Specification, Itinerary

## III. Modeling Out Loud

*Challenge:* next time you attend a requirements or design discussion, really listen! Do you hear domain specific language being used?

### The Power of Spoken Language

> It is vital that we play around with words and phrases, harnessing our linguistic abilities to the modeling effort, just as it is vital to engage our visual/spatial reasoning by sketching diagrams.

Examples

- Pidgin: a common language created between people of different language backgrounds come together for commerce!
- When people are talking, they naturally discover differences in interpretation and the meaning of their words, and they naturally resolve those differences.
- Lean into the discomfort! Think awkward conversations in intensive Spanish class in college. Ultimately, you end up more fluent than you would have been doing paper exercises.

> Play with the model as you talk about the system. Describe scenarios out loud using the elements and interactions of the model, combining concepts in ways allowed by the model. Find easier ways to say what you need to say, and then take those new ideas back down to the diagrams and code.

## IV. One Language, One Team

Don't try to "shield" business experts from the domain models

IMPORTANT
> If sophisticated domain experts don't understand the model, there is something wrong with the model.

### Extending the Language

- Specialized jargon WILL exist on both the dev and domain expert sides, but these are simply extensions to the shared language
- These dialects SHOULD NOT contain alternative vocabularies for the same domain that reflect diverging models

### Documents and Diagrams

**Good Use**: Sketch a diagram of three to five objects central to the issue at hand, and everyone can stay focused. Everyone will share a view of the relationships between the objects and, significantly, the objects' names. The spoken discussion can be more effective with this aid.

**Ineffective Use**: when people feel compelled to convey the whole model or design through UML (Unified Modeling Language)

> A lot of object model diagrams are too complete and, simultaneously, leave too much out. They are too complete because people feel they have to put all the objects that they are going to code into a modeling tool. With all that detail, no one can see the forest for the trees.

### Visual Limitations
- Attributes and relationships are only half the story of an object model
- Behavior of objects and the constraints on them are not easily illustrated

> In other words, a UML diagram cannot convey two of the most important aspects of a model: the meaning of the concepts it represents, and what the objects are meant to do. This needn't trouble us, though, because careful use of English (or Spanish, or whatever) can fill this role pretty well.

**The model is not the diagram --> a diagram's purpose is to help communicate and explain the model**

### Written Design Documents

**Two General Guidelines**

1. Documents Should Complement Code and Speech
2. Documents Should Work for a Living and Stay Current

**Extreme Programming**

- definition: no extra design documents at all and letting the code speak for itself
- PROS
   - motivates developers to keep the code clean and transparent
- CONS
   - overwhelms the reader with detail
   - behavior isn't obvious and meaning can be hard to convey

**Look for Meaning, Don't Get Lost in the Detail**
> Written documents need to illuminate meaning, to give insight into large-scale structures, and to focus attention on core elements. Documents can clarify design intent when the programming language does not support a straightforward implementation of a concept.

**Let Go of Stale Documentation**
> You may hear the UBIQUITOUS LANGUAGE changing naturally while a document is being left behind. Evidently the document does not seem relevant to people or does not seem important enough to update. It could safely be archived as history, but left active it could create confusion and hurt the project. And if a document isn't playing an important role, keeping it up to date through sheer will and discipline wastes effort.

** GOAL: By keeping documents minimal and focusing them on complementing code and conversation, documents can stay connected to the project.**

## V. Explanatory Models

The model that drives the design is one view of the domain, but it may aid learning to have other views, used only as educational tools, to communicate general knowledge of the domain.

### Example: Shipping Operations and Routes

- Uses a separate diagram (distinct from UML) to convey how cargo flows through a Route (in the UML)

Chapter Synopsis: *one model should underlie implementation, design, and team communication*
