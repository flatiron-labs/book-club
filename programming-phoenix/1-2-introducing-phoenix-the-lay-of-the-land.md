# ProgrammingPhoenix
# Introducing Phoenix

## Why Elixir?

- Fast
- Concurrent:
	- Multiple calls to DB

```
company_task  = Task.async(fn -> find_company(cid) end)
user_task     = Task.async(fn -> find_user(uid) end)
cart_task     = Task.async(fn -> find_cart(cart_id) end)
company = Task.await(company_task)
user = Task.await(user_task)
cart = Task.await(cart_task)
```

- Beautiful
	- Macros
	- Pipelines
		- no more `skip_before_filter`. Build pipelines for groups of routes that all just work

```
pipeline :browser do
  plug :accepts, [“html”]
  plug :fetch_session
  plug :protect_from_forgery
end
pipeline :api do
  plug :accepts, [“json”]
end
scope “/”, MyApp do
  pipe_through :browser
  get “/users”,     UserController, :index
end
scope “/api/“, MyApp do
  pipe_through :api
end
```

- Simple Abstractions
	- OO languages, inheritance is not rich enough abstraction
	- Example: Authentication (touches all parts of an app)
-  Interactive
- Scaling by Forgetting
- Processes and Channels
	- Elixir lightweight processes, can scale to hundreds of thousands

```
def handle_in("new_annotation", params, socket) do broadcast! socket, "new_annotation", %{
user: %{username: "anon"}, body: params["body"],
at: params["at"]
}
{:reply, :ok, socket}
end
```
- Reliable
	- Supervisor tree

## Who’s this book for?
- Programmers Embracing Functional Paradigm
- Rails Developers Seeking Solutions
- Dynamic Programmers Looking for a Mature Environment
- Java Developers Seeking More
- Erlang Developers Doing Integrated Web Development

## Lay of the Land
### Pipes and Segments
```
def inc(x), do: x + 1
def dec(x), do: x - 1

2 |> inc |> inc |> dec
```
- can chain function calls together into **pipes/pipelines** made up of **segments**
- takes the value on the left and passes it in as the first argument on the right
- pipelines are functions as well, you can make pipelines of pipelines

`connection |> phoenix`
- connection has all the info about the request
- phoenix is just a set of pipelines that modify it, until the end when a response is given from the connection
- **interesting this is the first thing they talk about**, **seems foundational**

### Layers of Phoenix

HTTP requests:
```
connection
|> endpoint
|> router
|> pipelines
|> controller
```

controllers:
```
connection
|> controller
|> common_services
|> action
```

actions:
```
connection
|> find_user
|> view
|> template
```

- common services implemented with **Plug**

	- In Phoenix, **limit side effects** => fns that touch and modify the outside world, calling fn with the same arguments always yields the same results
	- separate code that calls a server/database from code that transforms data
	- process data in the model
	- read/write data through the controller

### Dependencies
- Erlang
- Elixir
- Hex - elixir’s package manager
- brunch & npm for asset management
- Phoenix


### Routes
```
scope "/", Hello do
	pipe_through :browser
	get "/", PageController, :index
end
```

### Controllers
```
defmodule Hello.HelloController do
	use Hello.Web, :controller

	def world(conn, _params) do
		render conn, "world.html"
	end
end
```

### Pattern Matching
```
iex> {first, second, third} = {:lions, :tigers, :bears} {:lions, :tigers, :bears}
iex> first :lions
iex> {first, second, :bears} = {:lions, :tigers, :bears} {:lions, :tigers, :bears}
iex> {first, second, :armadillos} = {:lions, :tigers, :bears}
**** (MatchError) no match of right hand side value: {:lions, :tigers, :bears}

iex> austin = %{city: "Austin", state: "Tx"} %{city: "Austin", state: "Tx"}
iex> defmodule Place do
...> def city(%{city: city}), do: city
...> def texas?(%{state: "Tx"}), do: true
...> def texas?(_), do: false ...> end
```

#### Atom keys vs String keys
- External data cannot be safely converted into atoms because the atom table isn’t garbage collected.
- Match on string keys in your boundaries (controllers and channels), those will convert to atoms to be used everywhere else

## The Request Pipeline
- Web applications are just functions: URL => formatted HTML response string

### Plugs
- Specification for building applications for the web
- Consumes and produces `Plug.Conn` structs
	- **represents the whole universe**
- takes in a `conn` and returns a slightly modified `conn`
- **Plugs are functions**
- **Your web app is a pipeline of plugs**

### File Structure
`config` -> phoenix config
`lib` -> supervision trees and long running processes
`test` -> tests
`web` -> web related models, views, templates, and controllers

**web vs lib**
- web is hot reloaded
- lib for long running services: Phoenix PubSub, database connection pool, supervised processes

### Wrapping Up
- Web applications in Phoenix are pipelines of plugs
- The basic flow of traditional applications is endpoint, router, pipeline, controller.
- Routers distribute requests.
- Controllers call services and set up intermediate data for views.
