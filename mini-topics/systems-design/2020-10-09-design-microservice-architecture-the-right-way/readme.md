# Design Microservice Architectures the Right Way

> Speaker: Michael Bryzek

> Notes Author: Avidor Turkewitz

> Source: https://www.youtube.com/watch?v=j6ow-UemzBc

Building microservice architecture in certain ways can cause really painful problems. Example: Updating a url takes a long time to update. It's hard to tell if we have a good design until a couple of years down the road when we can see how it holds up and how hard/easy it is to update.

Tradeoffs: Near term velocity / future paralysis

## Microservice Misconception

- We can use the right language and framework for the problem
  - Reality: This gets real expensive
- Code generation is  evil (I don't get this)
  - Reality: ???
- Event log must be source truth
  - Reality: Events are good, but it's ok for services to be the system of record. Resources MUST end up on stream
- Devs can maintain no more than 3 services each
  -  Reality: It can be more

## APIs

Flow uses events and APIs (when to use each? - Events prefered, API if synchronous is needed)
API Definition
API definitions are in their own API (similar to what we have to IPC messages)

[API Builder](https://app.apibuilder.io/doc/) (OSS software at Flow) tool to identify breaking API changes.
- Auto gens routes
- Auto gen client lib
- Auto gen mock client for testing

## Databases

QUESTION: DOA?  Referenced UserDoa, but I don't know what DOA stands for

Databases belong to a service. They are private. Once other services connect,  there are issues.
Database config auto generated by a `dev` CLI to ensure consistency.
- Makes it easy to enforce something like 'no empty strings', must use NULL instead
- Save on global updates where nothing changes because they wrote the hashing check _once_ and they put it in the generator

Super simple config settings for the service.
- QUESTION: Could we trim down our teraform (terror form?) config to be more like this?

## Deploying

CD absolutely essential for microservices. Without it, you'll spend all your time deploying.

## Events

Only using API if something is needed synchronously.
Events are the JAM! Preferred use for both internal and external. "We have an amazing API, but please subscribe to our event streams instead."

Principles of events:
- First class schema for all events
- Producers guarantee at least once delivery
- Consumers implement idempotency

Producers:
- Hold journal (QUESTION: how hard/easy is this to implement?)
- Record operation with event
- 1 event per journal event

Consumers:
- Store new events in local db
- Process events
- Record failures

Events:
- Use API builder for this as well
- Streams are owned by one service (e.g. Compliance docs)
- Linter to ensure commonality between events

Journaling
- github.com/gilt/db-journaling
- declare simple retention policy

Producer Streams:
Don't need to specify name of stream (sounds like level of abstraction on top of railway...)

QUESTION: Talking about keeping local copy of data. We've found the pain point of this to be the backfill. How does flow handle that?

## Dependencies

How to keep dependencies up to date?
**Automatically** keep all dependencies up to date.
dependencies.flow.io
github.com/flowcommerce/dependency

## Wrap Up

Key takeaways:
- Design schema first for all APIs and Events (prefer events over API)
- Invest in automation (need to limit language and framework)
- Enable teams to write amazing and simple tests
