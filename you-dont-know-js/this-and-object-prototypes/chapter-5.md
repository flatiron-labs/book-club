# Chapter 5: Prototypes

## [[Prototype]]
- simply a reference to another object
- The default [[Get]] operation follows the [[Prototype]] link if requested property not on object
- iterating with `for...in` also returns properties located on prototype-linked objects
- end of the _normal_ [[Prototype]] chain is built-in Object.prototype

## Setting and Shadowing Properties 
* Shadowing: When a property ends up both on `myObject` itself and at a higher level of the [[Prototype]] chain (p. 88)

CASE 1 Existing data accessor property, change the value of existing property

CASE 2 If not present on object, traverse the [[Prototype]] chain.
  - if not found in chain, add property directly to the object
  - if present higher in the chain, weird stuff (1 of 3) happens

**Weird Stuff p. 88**

1. property IS found higher on chain and not read-only => new property added directly to object (shadowed property)
2. property IS found higher on chain but marked as read-only => no setting of the property occurs and no shadowing occurs
3. property IS found higher on chain and is a setter, the setter (property that calls a hidden function to set a value) will be called & no new property will be added and the setter won't be redefined. 

**Review of setters/getters**

```
var myObject = {
  get a() {
    return this._a_;
  },
  
  set a(val) {
    this._a_ = val
  }
}

```

Referring to weird stuff case #2
"If you however separate the illusion from the fact, and recognize that no such inheritance copying actually occured (see Chapters 4 and 5), it’s a little unnatural that myObject would be prevented from having a foo property just because some other object had a nonwritable foo on it." (p.89)

Example of whoops shadowing with `myObject.a++` on p.89; problem is that `++` is equivalent to `myObject.a = myObject.a + 1`

**Questions**
- Shadowing...why? When?


## "Class" & "Class" Functions
- all functions get public, nonenumerable property called `prototype` which is an arbitrary object (whoa)
- "the object arbitrarily labeled Foo dot prototype"
- any object created from the constructor call of a function will be prototype linked to this object. 
- reminder that there are no copies in JS, but objects end up [[Prototype]]-linked
- the creation of the link is sort of an accidental side effect

**Questions**
- Following rant on how prototypal inheritance is confusing and done more harm than good ==> do we agree? (p. 94)
- Argument that delegation is more accurate than inheritance


## "Constructors"
- `Foo.prototype` object has property called `.constructor` that refers back to the function
- `Foo` is no more a "constructor" than any other function; when you put `new` in front of a normal function call, that makes that function call a "constructor call"
- some bashing of "class" discussions in JS and simulations of class orientation
- you can replace a function's prototype
- the `.constructor` property does not mean was constructed by

**Questions**
- why define anything on the prototype rather than the function object itself? in other words, why not define a property that points to a function? `function Car() { this.hello = function(){console.log('hello')}}`
- on p. 107, author talks about the point of the [[Prototype]] mechanism and benefits of `Object.create` (linking and delegation instead of unnecessary complication of new, .prototype, and .constructor)

## (Prototypal) Inheritance
- Pre-ES6: with `Object.create` which creates a new object and links that object's internal [[Prototype]] to the object specified
- ES6+ Object.setPrototypeOf(Child.prototype, Parent.prototype) 
- Introspection: 
  - `instanceof` checks if prototype appears in an object's entire [[Prototype]] chain. Can be misleading.
  - `Foo.prototype.isPrototypeOf (a)` better method and avoids indirection 

## Fallbacks
- probably shouldn't rely on prototypes for fallbacks b/c too magical
- use the delegation design pattern instead (explicitly call the function on the ancestor object)

