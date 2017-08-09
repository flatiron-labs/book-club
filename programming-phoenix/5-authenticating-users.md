# Programming Phoenix Ch 5: Authenticating Users

## Dependencies

1. Add package to `mix.exs` under `defp deps`
2. Add package to applications list to ensure it starts with app

## More On Changesets
- `:empty` parameters instead of empty map to distinguish blank new changeset from empty form submission
- leveraging existing `changeset` within the `registration_changeset` for changeset composition
```
def registration_changeset(model, params) do model
|> changeset(params)
|> cast(params, ~w(password), [])
|> validate_length(:password, min: 6, max: 100) |> put_pass_hash()
end
```
- "Our changeset insulates our controller from the change policies encoded in our model layer while keeping the model free of side effects." (p.73)
- "Validations are a pipeline of functions that transform the changeset" (p.73)

## The Anatomy of a Plug
- section objective: turning authentication into a plug to make it available throughout system, add it to pipeline in router so other controllers can use it
- Two types of plugs
  - *Module Plugs*: provides two functions w/ configuration details, specified by module name
  - *Function Plugs*: single function, provide the function name as atom

### Module Plugs
- module plug must have two functions, `init` and `call`
- `init` happens at compile time; `call` happens at runtime
- all plugs take a `conn` and return a `conn`

### Plug.Conn Fields
- basically everything Rack would give you + this `assigns` concept

- **Q: What else can you and should you put into `assigns`?**

## Authentication Plug
- located in `web/controllers/auth.ex`
- **Q: Why here in a controller?** 
- add `:current_user` to `conn.assigns` so it is accessible downstream, in controller and view 
- begin with writing authenticate function in each controller...
- note use of halt() (like ruby return?) to stop downstream transformations 

- after refactoring,  write a function plug to authenticate to put in the controller plug pipelines

### Function Plugs
- any function that receives the connection and set of options and that returns the connection
- "None of these features relies on magical inheritance mechanisms, only our explicit lists of functions in our plug pipelines." (p.81)
- "Plug pipelines explicitly check for halted: true between every plug invocation, so the halting concern is neatly solved by Plug." (p.81)
- macro expansion(???) -- part of compilation 
- **Q: What magical inheritance are they referring to? In Rails in the simplest form, you'd write a helper and a sessions controller...**

## Logging In
- review of `assign` on the `Plug.Conn` struct
- put user_id in session // sounds familiar
- put `current_user` in assigns (Q: seems to duplicate the plug behavior? What else would need this downstream?)
- configure_session(renew: true) to protect against session fixation attacks
- New controller, view, templates. Can pass an empty plug conn struct instead of a changeset when building forms not backed by changeset (login or search) // also similar, just instead of a model object, use a changeset
- logout similar // destroy the session, wipe out the `user_id` from session
