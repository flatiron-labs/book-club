# Chapter 4: Ecto and Changesets

_In which we replace our in-memory storage with a database without changing any controller code (!!)_

![](https://media.giphy.com/media/12mgnOzTJzwtjy/giphy.gif)

## What is Ecto?

- It's Elixir's persistence framework
- It's a _wrapper_
- Intended for _relational_ databases like PostgreSQL
- Ships with an "encapsulated" query language
- Composable queries
- Tedious, but reliable/predictable

Some alternatives: [https://github.com/h4cc/awesome-elixir#orm-and-datamapping](https://github.com/h4cc/awesome-elixir#orm-and-datamapping)

Changesets:  
- encapsulates "whole process of receiving external data, casting and validating it before writing it to the database."


### Questions:

1. What is an "encapsulated" query language?
    - encapsulates entire process of receiving, casting, and validating external data before writing it to db


## Migrations

Ecto.Migration API - very similar to Rails

Blog post on running migrations in production: [http://blog.kate-travers.com/ecto-migrations-on-production/](http://blog.kate-travers.com/ecto-migrations-on-production/)

## OTP

Casually mention OTP on page 56 like it's nbd.

OTP: "layer for managing concurrent, distributed services"

Example: Phoenix uses OTP to start and supervise Ecto repositories w/ named process: `Repo`

`Repo` represents our database

## Building Forms

More on changesets:
- "Customized strategy" for handling different kinds of changes
- Manage record changes
- Cast parameters
- Perform validations
- Composable
- Allow for multiple "update policies"
- "Policy segregation"

NEW: don't call `changeset` directly, instead wrap it in a function for a clean interface

- Changesets validate AND track changes

> Ecto is using changesets as a bucket to hold everything related to a database change, **before and after persistence**.


## EXERCISE

[https://github.com/ktravers/food](https://github.com/ktravers/food)


## Resources

1. [Ecto](https://hexdocs.pm/ecto/Ecto.html)
2. [Ecto.Repo](https://hexdocs.pm/ecto/Ecto.Repo.html)
3. [Ecto.Query](https://hexdocs.pm/ecto/Ecto.Query.html)
4. [List of Elixir ORMs, data mappings](https://github.com/h4cc/awesome-elixir#orm-and-datamapping](https://github.com/h4cc/awesome-elixir#orm-and-datamapping)
5. [Daily Drip Ecto tutorial](https://www.dailydrip.com/topics/elixir/drips/ecto-basics)
6. [Brad Urani, "ActiveRecord vs. Ecto: A Tale of Two ORMs" (RailsConf 2016)](https://youtu.be/_wD25uHx_Sw)
