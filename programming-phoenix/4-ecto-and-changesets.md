# Chapter 4: Ecto and Changesets

## Ecto

### Understanding Ecto (p53)

- It's a _wrapper_
- Intended for _relational_ databases like PostgreSQL
- Ships with an "encapsulated" query language
- Composable queries
- Tedious, but reliable/predictable

#### Questions:

1. What is an "encapsulated" query language?
    - encapsulates entire process of receiving, casting, and validating external data before writing it to db


### Defining the User Schema and Migration (p55)

- Ecto DSL specifies fields in a struct + mapping from fields <> db tables
- What is a model? (p57) Not a thing anymore as of Ecto v1.1 ([blog post](http://blog.plataformatec.com.br/2015/12/ecto-v1-1-released-and-ecto-v2-0-plans/))
- "This is a Bad Idea" p58 (we get it)


#### Questions:

1. Virtual fields seem cool (ex. `password` field)
    - Intermediate field
    - Not persisted to db
2. Contradiction on p56 - don't worry about plugins/packages adding/removing functionality?
    - Except example just showed us how to add plugins...
    - Ok bc they're not external packages?

### Building Forms (p60)

Changesets:  
- Manage record changes
- Cast parameters
- Perform validations

- "Customized strategy" for handling different kinds of changes
- Composable
- Allow for multiple "update policies"
- "Policy segregation" (p61)

#### Questions

1. Second Parameter `:empty` - is this still a thing?


### Creating Resources (p64)

- Changesets validate AND track changes

> Ecto is using changesets as a bucket to hold everything related to a database change, **before and after persistence**.
