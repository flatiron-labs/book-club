# Programming Phoenix Ch 9: Watching Videos

## Watching Videos

p158: Separate controllers for logged-in vs. public video view pages

p159: Use view to define "view helper" functions (ex. `player_id(video)`)

Q: What is `get_in`? Described on page 160 as a "map that returns the `id` key with its value"

## Adding Javascript

### Brunch (p160)

- build tool written in Node.js
- used to build, transform, and minify JS
- also handles all other app assets (CSS, images)
- lives in `web/static`
- uses ES6 by default
- configured in `brunch-config.js`

p161:

Anything that doesn't need to be transformed by Brunch, put inside `assets`. Those assets will get copied as-is to `priv/static`.

Treat `app.js` like a manifest. Use it to import dependencies.

p162: By default, Phoenix apps run `brunch watch --stdin` on start

## Creating Slugs (p164)

`alter table` migration uses the `alter` macro, which handles up and down migrations

## Extending Phoenix with Protocols (p167)

`Phoenix.Param` protocol

## Extending Schemas with Ecto Types (p169)

Custom types live in `lib` dir

p170

Q: customizing primary key?
