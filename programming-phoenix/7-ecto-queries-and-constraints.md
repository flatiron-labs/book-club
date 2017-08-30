# Chapter 7 - Ecto Queries and Constraints

Migrations still similar to Rails. When changing a col though, need to use `alter table(:table_names)`.

By adding reference column, ensure that the reference exists - enforced

Seed data similar. Best practice is to error out if there is an issue or if we go against constraints. 

Can write a query and call it all at once with `from`
```elixir
Repo.all from c in Category, select: c.name
```

Return a tuple by specifying multiple selects in `{}`:
```elixir
Repo.all from c in Category,
  order_by: c.name,
  select: {c.name, c.id}
```

Query can also be built without being called. 

```elixir
import Ecto.Query
alias Rumbl.Repo
alias Rumbl.Category
query = Category
query = from c in query, select: {c.name, c.id}
query = from c in query, order_by: c.name
# query built ^ but not called

Repo.all query
# query called ^
```

This appears to come from [Ecto.Query](https://hexdocs.pm/ecto/Ecto.Query.html#from/2)
`from` is weird. When piping, the first arg is queryable, but when writing inline, the syntax is a bit odd by using `in` after the first arg. 
This is some meta programing that Phoenix does. 

`Repo.one(from u in User, where: u.username == ^username)`
Expects ONLY ONE RESULT, not the _first_ result

QUESTION: Why do we need that pin operator?
Pin operator does interpolation for us so Ecto can scrub them and safely use them. 

Standard query operators like we've seen in SQL and AR

Queries can build on top of each other:
```elixir
import Ecto.Query
alias Rumbl.Repo
alias Rumbl.User
users_count = from u in User, select: count(u.id)
j_users = from u in users_count, where: ilike(u.username, ^"%j%")
```

Piping queries:
```elixir
User |>
  select([u], count(u.id)) |>
  where([u], ilike(u.username, ^"j%") or ilike(u.username, ^"c%")) |>
  Repo.one()
```

Fragments - The ability to run some direct SQL (but Elixir, is still doing some scrubbing with the pin):
```elixir
from(u in User, where: fragment("lower(username) = ?", ^String.downcase(uname)))
```
Can still run raw SQL with `Ecto.Adapters.SQL.query()`:
```elixir
Ecto.Adapters.SQL.query(Rumbl.Repo, "SELECT power($1, $2)", [2, 10])
```

Preloading. This can be done in the initial query, does not need to be a separate step:
`user = Repo.one from(u in User, limit: 1, preload: [:videos])`

Constraints:
'constraint' - set in the db level
'constraint error' - thrown directly from the db
'changeset constraint' - allows ecto to convert a constrain rror to a changeset error message
'changeset error message' - human readable message

Ecto prefers a balance between db constraints and coded constraints?

Validate in the db with `create unique_index(:users, [:username])` and then in elixir in the changeset with `|> unique_constraint(:username)`. This will ensure that we do not hit the DB at all, but we still have a safety if something went wrong. 

We can also set constraints like `assoc_constaint` to ensure an associations and even set what happens when a delete would break this assoc. 

Interesting Phoenix philosophy -> If the user cannot fix it, let it crash. 