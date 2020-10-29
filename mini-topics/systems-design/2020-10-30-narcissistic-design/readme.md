# Narcissistic Design

> Speaker: Stuart Halloway

> Notes by: Avidor Turkewitz

> Source: https://www.youtube.com/watch?v=LEZv-kQUSi4

Oh god. This whole thing is wayyyyy to saracstic.

Making your code complicated means you are needed as a programer here.

## Setter methods

An object is in a good state after its constructed. After that there is an issue because it might not be in a valid state anymore.

Undermine interface.
Setters may not validate?

## Prefer APIs over Data

### Data

- Data is immutable
- It lasts after the code runs and we don't need to rely on the code working RIGHT NOW.

### API

- Temporal coupling
- Same language (in terms of libraries?)

## DSL

This can be hard to work with?
Best to use an API or if possible a data modle


## Always connect, never enque

e.g. Active record makes it super easy to have all objects connected. This can for sure lead to issues when we assume that data is there.

## Create Abstractions for information

Be careful about wrapping up all our data?

## Use static typing across subsystem boundries

Throwing errors when you receive the wrong data can be very brittle if you're only an intermediate system

Throwing a lot of different errors in different places isn't helpful because it's broken either way?

## Put language semantics on the wire

Be careful about putting languages on the wire like protobuff?
It now forces that language all over the place. This is more complex than something like a programing language which is encapsulated to where it's running.
JSON is universal.
Some issues with JSON in that everything is a string (dates...)

## Write lots of unit tests

There's a world where some of this can be automated maybe? Auto gen inputs instead of hand writing them?

Be careful about too many unit tests
English language DSL, he is not a fan. It takes extra time to write it.

## Update information in place

Good with limited resources (not a lot of memory, storage, or processing). If these are not factors though, it's harmful because it means this data could be getting mutated anywhere because it's shared. Not good for sharing between processes.

Immutable data helps make things simple. It also allows us to see what happened before if we need to.

## Leverage context

Don't do things implicitly???

## Worst Examples

- ORMs
- Build tools
