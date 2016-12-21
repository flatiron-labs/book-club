# You Don't Know JS - Scopes and Closures

## Chapter 4: Hoisting

Hoisting is one subtlety of variable scope attachment, and it has to do with where variables are declared within a scope.

Remember, scripts are not _necessarily_ interpretted line-by-line top-down in order. That's because code gets run through compiler before it's interpretted, AND during compilation, variable declaration are 1) found and 2) associated with a scope.

** Declarations are processed first** before any code is executed.

Chicken vs. Egg examples
- declaration == egg
- assignment == chicken

```javascript
a = 2;

// actually interpretted as two tasks:
var a; // processed during compilation phase
a = 2; // left in place for execution phase
```

**Variable and Function declarations** are moved to top of their enclosing scope code, aka "hoisted".

#### Important nuances:

1. Only declarations are hoisted. Assignments and/or executeable logic are **left in place**.
2. Function expressions are NOT hoisted.
3. **Functions are hoisted first**, then variables

#### Related:
- Ruby hoists stuff too!
- Can cause some weirdo bugs

## Chapter 5: Scope Closure

_"Closure is all around you"_ (p48)

^^ You're already using it, so you better understand it.

Definition: "Closure is when a function is able to remember and access its lexical scope even when that function is executing outside its lexical scope." (p48)

In other words, closure is function + connection to its scope.

When nested function returned from outer function, it has knowledge of everything around it when it was created. But when called later, it'll use that same knowledge - - - not anything from where it was called from.

Good example from http://hostiledeveloper.com/2014/04/13/closures.html (c/o @stevennunez):

```javascript
def funky_scope
  x = 5
  -> () { puts x }
end
l = funky_scope
l.call # => 5
x = 30
l.call # => 5
```

##### Side tangent:
- Faulty garbage collection can lead to memory leaks.
- Browsers like Chrome are a little overzealous about garbage collecting, which is why sometimes you won't have access to things you should have access to inside a debugger

#### Modules
- leverage closure
- super powerful

#### Modern Modules
- Pattern handled by module dependency loaders/managers
- friendly API

#### Future Modules
- First-class syntax support for the concept of modules
- ES6 treats a file as a separate module
