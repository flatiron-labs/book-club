# Programming Phoenix Chapter 12: Observer and Umbrella

# Key Concepts
"**Umbrella projects** allow you to develop and test multiple child applications in isolation side by side while providing conveniences for configuring and building them only once"

# Observer
- `:observer.start` from IEx session
- Introspect all running processes in app
- Look for a convenient/logical separation point 

# Umbrellas
- Parent directory defines
  - shared configs
  - dependencies
  - apps with child applications

- Elixir configures project to use config, deps, and build paths from parent application

- Can treat the service as though someone else built it; super clean interface

# Wrapping Up
- Umbrellas are an Elixir construct

Q: In what ways is the Umbrella approach similar to domain-driven design? When, if ever, would you favor microservices? 

Q: Isn't this still just a monolith? Or does it solve the problem of code isolation versus inability to search cross-repos? 

Q: If we drew parallels to ruby or js, what would they be? 
  - Writing your own gem to import into a Rails project
  - Writing your own npm package and including it from the npm registry

Q: Umbrellas, what do you think?

Q: Why did we call IDE v2 the ide_umbrella?

# Umbrella Info from Elixir Docs
"Don’t drink the kool aid

Umbrella projects are a convenience to help you organize and manage multiple applications. While it provides a degree of separation between applications, those applications are not fully decoupled, as they are assumed to share the same configuration and the same dependencies.

The pattern of keeping multiple applications in the same repository is known as “mono-repo”. Umbrella projects maximize this pattern by providing conveniences to compile, test and run multiple applications at once.

If you find yourself in a position where you want to use different configurations to different applications in the same umbrella or to use different dependency versions, then it is likely your codebase have grown beyond what umbrellas can provide."

Source: [Dependencies and umbrella projects](https://elixir-lang.org/getting-started/mix-otp/dependencies-and-umbrella-apps.html#dont-drink-the-kool-aid)
