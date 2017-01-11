# You Don't Know JS - this and Object Prototypes

## Chapter 3: Objects (p35)

Constructed form syntax:
- says you can only add properties one by one
- what about `new Example({prop1: 'value', prop2: 'value'})` ?

### Six primary/language types: (p36)

1. string
2. number
3. boolean
4. null
5. undefined
6. object

NOTE: **simple primitives (string, boolean, number, null, and undefined) are not objects**

WAT alert:

> `typeof null` [returns] the string "object" in‐correctly (and
> confusingly). In fact, null is its own primitive type.


## Object Subtypes (p37)

### Complex primitives

Function is a subtype of object: "callable object"
- first class objects
- normal objects with callable behavior semantics

Arrays also object with special behavior
- organization of "contents" (?) more structured than your general object, so gets special distinction

### Built-in Objects/Functions (p37)

• String
• Number
• Boolean
• Object
• Function
• Array
• Date
• RegExp
• Error

- Sames names as primitives, but not necessary directly related
- Can be used as a constructor

p38 (top paragraph):

> The primitive value "I am a string" is not an object, it’s a
> primitive literal and immutable value. To perform operations
> on it, such as checking its length, accessing its individual
> character contents, etc., a String object is required.

Seems like this is saying you can't perform operations on a primitive. But then how do you explain:

```javascript
> var str = 'hello'
undefined
> str.length
5
```

Answer: Javascript automatically coerces a string primitive to a `String` object when necessary. How does it know when that's "necessary"?

Also community loves relying on this coercion? Why not just play it safe / use language as intended and use the constructed Object form?

Above is same for number primitive + Number obj and boolean primitive + Boolean obj.

BUT more inconsistencies:
- `null` and `undefined` have no object form, only primitives
- Date only has constructor, no primitive

## Contents (p39)

Properties: object values that exist at specific, named location
- stored in implementation-dependent way, so may not be stored in object container
- instead, property names are stored in obj container
- property names == pointers/references to where the values are stored
- property names are _always_ strings


### Key access vs. property access (p39)

```javascript
myObject.a; // key access
myObject["a"]; // property access
```

- Can be used interchangeably
- "Method access": when accessing property value that's a function
- ^^ kind of a misnomer

## Arrays (p43)

Adding named properties to an array: something we probably do fairly often, but I've never noticed/thought about before

RED FLAG:

> Be careful: if you try to add a property to an array, but the
> property name looks like a number, it will end up instead as
> a numeric index (thus modifying the array contents):

## Duplicating Objects (p44)

ES6 standard for shallow copy: `Object.assign(...)`
- iterates over all the enumerable, owned keys on the source object(s)
- copies them (via = assignment only) to the target
- returns the target

## Property Descriptors (p46)

- writeable
- configureable
- enumerable

### Configurable (p48)

- when configurable:true, object can be modified via `defineProperty(..) utility
- configurable:false is a one-way action; can't undo bc object is unmodifiable now
- when configurable:false, can't delete properties
- writeable:false + configurable:false is essentially a constant

More weirdness:
- when configurable:false, you can still change writeable from true to false

## Immutability (p50)

`Object.preventExtensions()`
- prevents extensions
- other properties not changed or locked

`Object.seal()`
- prevents extensions
- configurable:false

`Object.freeze()`
- prevents extensions
- configurable:false
- writeable:false

## Existence (p56)

robust way to check if property exists: `Object.prototype.hasOwnProperty.call(myObject,"a")`

^^ checking for property name, not property value

## Iteration (p59)

NOTE:

> order of iteration over an object’s properties is not
> guaranteed and may vary between different JS engines.


