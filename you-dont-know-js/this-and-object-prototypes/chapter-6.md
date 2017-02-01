# You Don't Know JS - this and Object Prototypes

## Chapter 6: Behavior Delegation (p113)

Chapter 5 recap: why so complicated?

> "...it’s not a surprise that most JS developers never dive this deep,
> and instead relegate such mess to a “class” library to handle it for them."

Objected oriented JS (OOJS):
- confusing
- misleading

Delegation oriented JS (OLOOJS):
- "objects linked to other objects"
- simpler
- more straight forward

### Composition Over Inheritance

Change the way you build relationships between objects

### Delegation-Oriented Design (p114)

> "...the actual mechanism, the essence of what’s important to the
> functionality we can leverage in JavaScript, is all about
> objects being linked to other objects."

Focus on **"behavior delegation design pattern"**

Side note: some OO principles, like _encapsulation_ are still useful/compatible w/ DO design

### Delegation Theory (p115-116)

1. Define base object with utility methods that can be delegated to
2. Define object linked to base object
  - this object has its own specific data/behavior
  - but can also delegate to base object methods

p117: OLOO Pattern encourages easier-to-maintain code:

> "This design pattern calls for less use of general method names
> that are prone to overriding and instead more use of descriptive
> method names, specific to the type of behavior each object is doing.
> This can actually create easier to understand/maintain code, because
> the names of methods (not only at the definition location but strewn
> throughout other code) are more obvious (self-documenting)."

p118:

> "...think of objects side by side, as peers, with any direction of
> delegation links between the objects as necessary."

### Mutual delegation IS NOT ALLOWED (p118)

Error if you try to bidirectionally link two objects

Why?

> "...it’s more performant to check for (and reject!) the infinite
> circular reference once at set-time rather than needing to have the
> performance hit of that guard check every time you look up a property
> on an object."

### A whole bunch of pages dragging OOJS...

p131:

> "**OLOO better supports the principle of separation of concerns**,
> where creation and initialization are not necessarily conflated
> into the same operation."

^^ Agree? Examples?

### Separation of concerns

Separate constructor and initializer
- in Ruby: `allocate` + `initialize`
  - `allocate` == give me an object
  - `initialize` == create this object

example p129
1. create Widget
2. call `setup` on this new object
3. `setup` doesn't happen dynamically at runtime

### Introspection

Approaches:
- Check prototype, but awkward/unintuitive
- Use duck typing (some downfalls, specifically Promises)
- `Foo.isPrototypeOf` => OLOO approach, so best

### Reality Check

Teaching this:
- in real world, we all use libraries
- in real world, students will see Classes
- Steven more likely to teach Classes
