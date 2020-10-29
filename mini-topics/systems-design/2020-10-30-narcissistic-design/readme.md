# Narcissistic Design

> Speaker: Stuart Halloway

> Notes by: Avidor Turkewitz

> Source: https://www.youtube.com/watch?v=LEZv-kQUSi4

DISCLAIMER: Oh god. This whole thing is wayyyyy too sarcastic. Notes will reflect the point that I believe he is trying to get across to the best of my ability and _not_ what he actually says.

Simple code is good and makes things easier to understand but there are a whole bunch of anti patterns out there that seem to have become a standard in some ways. The following are a list of anti-patterns:

## Setter methods

An object is in a good state after its constructed. After that there is an issue because it might not be in a valid state anymore. (Java)
Setter methods undermine the constructor interface.

**Question: Does this apply to something like ActiveRecord where the validators run for any setting?**

## Prefer APIs over Data

### Data

- Data is immutable
- It lasts after the code runs and we don't need to rely on the code working RIGHT NOW.

### API

- Temporal coupling
- Same language (in terms of libraries?)

### Example: Running tests

When a test runs, if we need to use a special API to read them, that's a lot of coupling. If the results are just dumped to a file though, anything can pick it up and read it at any time.

## DSL

This can be hard to work with?
Best to use an API or if possible a data model
Example: SQL DSL

**QUESTION: Is SQL is so bad how come we don't have something better now? Is that what GraphQL is?**

## Always connect, never enqueue

e.g. Active record makes it super easy to have all objects connected. This can for sure lead to issues when we assume that data is there.

## Create Abstractions for information

Be careful about wrapping up all our data. When we create special objects that are just data at their core, they become harder to work with and we need special/custom libraries to work with them.

**QUESTION: What about all the _extra_ functionality this adds? Are people wrapping data without _any_ value add?**

## Use static typing across subsystem boundaries

Throwing errors when you receive the wrong data can be very brittle if you're only an intermediate system
Throwing a lot of different errors in different places isn't helpful because it's broken either way?

## Put language semantics on the wire

Be careful about putting languages on the wire like protobuff?
It now forces that language all over the place. This is more complex than something like a programing language which is encapsulated to where it's running.
JSON is universal.
Some issues with JSON in that everything is a string though (e.g. dates...)

## Write lots of unit tests

There's a world where some of this can be automated maybe? Auto gen inputs instead of hand writing them?

Be careful about too many unit tests
English language DSL, he is not a fan. It takes extra time to write it. We spend more dev hours worrying about the best english lang syntax for tests than we need to and this is a waste of time.

## Update information in place

Good with limited resources (not a lot of memory, storage, or processing). If these are not factors though, it's harmful because it means this data could be getting mutated anywhere because it's shared. Not good for sharing between processes.

Immutable data helps make things simple. It also allows us to see what happened before if we need to.
Immutable examples:
- Elixir
- React

## Leverage context

Don't do things implicitly???
Note: I'm not super sure I understood this one

## Worst Examples of these Anti Patterns

- ORMs
- Build tools
