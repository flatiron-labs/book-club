# Programming Phoenix Chapter 8: Testing MVC

## Testing Philosophies
- Fast 
- Right level of isolation 
- DRY
- Repeatable

Supported in Phoenix by
- clean contracts between layers of app
- focus on immutability, concurrency, and speed. Functional programming ftw

## Definitions
**Unit Test** - exercises function for one layer in application
**Integration Test** - focuses on how many different layers interact
**Acceptance Test** - multiple actions work together 
**Performance Testing**

## Understanding ExUnit
- main macros
  - setup ~ "before each"
  - test ~ "it"
  - assert ~ "expect"

## Using Mix to Run Phoenix Tests
- `mix test`
- `ConnCase` module - provides a lot of test setup helpers 
- use a database transaction for sync tests so that it'll run on clean slate
- plenty of test helpers such as `html_response` and `json_response`

## Integration Tests
- finding the right level of isolation
- fully test the route through the endpoint
- file for test helpers rather than...factories?
- "For simple data with a few well-defined relationships and mostly static attributes, you might find that simple functions work better." (p. 135)
- 
- modifying code to make it more testable with a bypass mechanism
- **tagging** tests to run and how to set up the seed data (p. 138)
- "Writing negative tests is a delicate balance. We don’t want to cover all possible failure conditions. Instead, we’re handling concerns we choose to expose to the user, especially those that change the flow of our code" (p. 140)

## Unit Testing plugs
- lot of set up to get `bypass_through` working
- `bypass_through` allows you to send a connection through the endpoint, router, and desired pipeline but bypass the route dispatch
- test login, logout, the call method

## Testing Views and Templates
- just functions. seem to be testing strings...is that worth it?

## Splitting Side Effects in Model Tests
- Without side effects: testing changesets validity
- because the tests are functional, they can be concurrent
- With side effects: repository tests. Rationale is to test some error conditions as close to breaking point as possible, even though the integration tests probably handle 
