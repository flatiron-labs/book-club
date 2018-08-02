# Chapter 4: Ecto and Changesets

_In which we replace our in-memory storage with a database without changing any controller code (!!)_

![](https://media.giphy.com/media/12mgnOzTJzwtjy/giphy.gif)

## What is Ecto?

It's Elixir's persistence framework.

Intended for relational databases.

Some alternatives: [https://github.com/h4cc/awesome-elixir#orm-and-datamapping](https://github.com/h4cc/awesome-elixir#orm-and-datamapping)

Changesets: encapsulates "whole process of receiving external data, casting and validating it before writing it to the database."


## Migrations

Ecto.Migration API - very similar to Rails

Blog post on running migrations in production: [http://blog.kate-travers.com/ecto-migrations-on-production/](http://blog.kate-travers.com/ecto-migrations-on-production/)

## OTP

Casually mention OTP on page 56 like it's nbd.

OTP: "layer for managing concurrent, distributed services"

Example: Phoenix uses OTP to start and supervise Ecto repositories w/ named process: `Repo`

## Building Forms




## Resources

1. [Ecto](https://hexdocs.pm/ecto/Ecto.html)
2. [Ecto.Repo](https://hexdocs.pm/ecto/Ecto.Repo.html)
3. [Ecto.Query](https://hexdocs.pm/ecto/Ecto.Query.html)
4. [List of Elixir ORMs, data mappings](https://github.com/h4cc/awesome-elixir#orm-and-datamapping](https://github.com/h4cc/awesome-elixir#orm-and-datamapping)