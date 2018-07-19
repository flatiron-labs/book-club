## The Lay of the Land
- Web server as function metaphor
### Simple Functions
- In Elixir can chain function calls together like below. 
- `|>` is the pipe opeartor or "quack pipe"
```
def inc(x), do: x + 1
def dec(x), do: x - 1

2 |> inc |> inc |> dec
```
- Composing functions together creates  **pipes/pipelines**
- **Segments** are the individual functions between the pipes. 
- Value on the left passed as first argument to next segment
- Pipelines are functions so you can make pipelines of pipelines
- We can think of a phoenix program as `connection |> phoenix` where *connection* is a struct (map with known fields) with all the user's request info and *phoenix* is a series of pipelines modifying *connection* until it ends up with the response in it 

### The Layers of Phoenix

##### HTTP requests:
```
connection
|> endpoint
|> router
|> pipelines
|> controller
```
- Pipelines group functions together to handle common tasks. For example, you could have one for browser requests and one for JSON requests

##### Controllers:
```
connection
|> controller
|> common_services
|> action
```
- Controllers are pipelines of like functions grouped together
- Common services are implemented with *Plug*, which will come up later
- Below is an example action

##### Actions:
```
connection
|> find_user
|> view
|> template
```
- **Context** - API which side effects should be limited to. Basically any functions that touch and possibly change the outside world
  - Context called from controller so functions in models and views can be kept pure (calling function with same arguments always yields same results)
- process data in model
- read/write data in context
- access context through controller
- *Ecto* is the persistence layer and separates code that has side effects from code that's just transforming data

### Installing Your Development Environment
#### Dependencies
- Erlang - base programming virtual machine
- Elixir
- Hex - package manager
- Postgres - default for Ecto
- Node.js - asset management
- Phoenix

#### Hello World Project
- Can run server using `mix phx.server` or inside Interactive Elixir using `iex -S mix phx.server`
- `.ex` extension is for compiled Elixir files
##### Router:
```
scope "/", Hello do
  pipe_through :browser
  get "/hello", HelloController, :world
  get "/", PageController, :index
end
```
- Pretty similar to ruby
- `pipe_through :browser` is a macro that handles housekeeping for all common browser-style requests

##### Controller:
```
defmodule Hello.HelloController do
  use Hello.Web, :controller

  def world(conn, _params) do
    render conn, "world.html"
  end
end
```
- `use HelloWeb, :controller` is for using Phoenix Controller API

##### View:
```
defmodule HelloWeb.HelloView do
  use HelloWeb, :view
end
```
- code to render template

##### Template:
```
<h1>From template: Hello world!</h1>
<h1>Hello <%= String.capitalize(@name) %>!</h1>
```
- `.eex` templates seem a lot like `.erb`

### Pattern Matching
- `=` in Elixir mean "make the thing on the left match the thing on the right"
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
- `=` operator can be used to take data structures apart (city example above) or to test (texas? example)
- Can destructure deeply nested data structures with precision

#### Atom keys vs String keys
- External data cannot be safely converted into atoms because the atom table isn’t garbage collected.
- So instead match on string keys and then application boundaries (ie. controllers and channels) will convert into atom keys, which are used everywhere else

### The Request Pipeline
- Web applications are like big functions. Each qeb request is a function call where URL is the arg. Returned response is a formatted string
- Goal can then be viewed as understanding how functions are composed to make the one big function call that handles each request
- **Plugs**
  - Specification for building applications that connect to the web
  - Consumes and produces `Plug.Conn` structs, which represents whole universe of given request
  - Takes in a `conn` and transforms it slightly until eventually sent back to user
  - *Plugs are functions*
  - *Your web app is a pipeline of plugs*

#### Phoenix File Structure
```
├── assets
├── config
├── lib
├──── hello
├──── hello_web
├── test
```
- `assets` - JS/CSS
- `config` - Phoenix configuration
- `lib/hello` - supervision trees and long running processes
- `lib/hello_web` - web-related code (controllers, views, templates, etc)
- `test` - tests

#### Endpoints
- Where web server hands off connection to application code
- Endpoint is a `Plug` made up of other Plugs
- Can have more than one endpoint -> umbrella project?

#### Controllers, View, Templates
- Controllers make data available in the connection for consumption by view
- View substitutes values for a template

### Wrapping Up
- Web applications in Phoenix are pipelines of plugs
- Flow of traditional app is:
  - request -> endpoint -> router -> pipeline -> controller
- Routers distribute requests.
- Controllers call services and set up intermediate data for views.
