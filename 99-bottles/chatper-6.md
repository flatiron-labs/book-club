## Chapter 6 - Achieving Opennes

Suggests modifying `quantity` and `container` up front.

**Question: Wasn't that an option _before_ we broke out this new class?**

### Consolidating Data Clumps

Data clump code smell - the situation in which several (three or more) data fields routinely occur together.

Combine `quantity` and `container` into the `to_s` method on `BottleNumber` to clean this up and make the code look much neater.

### Making Sense of Conditionals

> Fowler offers several curative refactoring recipes. The two main contenders are Replace Conditional with State/Strategy and Replace Conditional with Polymorphism.

- Replace Conditional with State/Strategy
  - Breaks conditional up into smaller objects arranged in composition
- **Replace Conditional with Polymorphism**
  - Creating one class with defaults and sub classes for the branches using inheritance

**Question: Did anyone try the strategy pattern?**

The book suggests if you're not sure which solution is best (or you don't even know the best solution options for the given code smell), then google the refactoring techniques and try them all and choose the best.

**Question: Is it practical to take that much time for this? Or does it make more sense to just pick which ever you think will be right and leave it at that? You can always change the pattern if need be.**

### Replace Conditionals with Polymorphism

The sender does not know (or care) what object it is sending it's messages to.

This will decrease the conditionals, but increase the number of classes and dependencies.

We can identify special cases by looking at the conditionals:
- `if number == 1`
- `if number == 0`

Start by copying all methods that check for `0` into their own class, `BottleNumber0`.

We now have to create a factory (code that is responsible for creating instances of the correct class) to determine when `BottleNumber` is needed and when `BottleNumber0` is needed.

> The next goal was to reduce the subclass' conditional to its true branch, and the superclass' to its false .

> By refusing to be aware of the classes of the objects with which you interact, you grant others the freedom to alter your code’s behavior without editing its source.

*Comment: I really like the idea that something we should really be thinking about is how to empower others modifying this code in the future. This highlights in well.*

Repeat steps for a `BottleNumber1` class and make the factory a case statement (now it looks a bit like shameless green...)

We can still see there are 3 types of bottles and that bottles 2-99 are most similar with 0 being _more_ different than 1 because it overrides more methods (3) from it's parent class.

Our factory only has three cases (0, 1, and else) as opposed to four in shameless green (0, 1, 2, and else). The difference here is that our polymorphic bottle classes know how to talk about _bottles_ and not _verses_. Shameless green needed 4 cases because bottle 1 shows up in verse 2. I think this is the same reason that we decided not to code the 6 pack scenario into shameless green because for a special change like that, we would need to update verse 6 and the proceeding verse (7) because bottle 6 shows up there as well.

### Transitioning Between Types

`successor` is a problem because it violates the Liskov Substitution Principle. It returns an integer rather than an instance of the same class (or similar class in the case of polymorphism).

To eliminate this violation, `successor` needs to interact with the factory (which is not easily accessed as things currently stand):
- Move `bottle_number_for` to be a class method, `BottleNumber#for`.
- Use this new method in verse to get the next bottle
- Allow `#for` to accept either a number _or_ a `BottleNumber` so that we can keep doing one line changes.
- Return specific bottles in the successor methods
- Update verse to just use `bottle_number.successor`
- Remove the guard clause from `#for`

*We seem to create a lot of intermediate changes to be able to keep doing the 'on line changes' system*

### Making the easy change

If we ignore that the factory isn't open, we can add a class for bottle 6 to complete the task.

**Question: Why is it OK to ignore that the factory is not open? When coding on our own, how can we make this decision confidently?**

First, update the tests, then add the `BottleNumber6` class with special `quantity` and `container` methods, and finally update the factory. Done!

### Defending the Domain

While overriding `to_s` for `BottleNumber6` could have passed the tests, it now appears to be telling some lies:
1. `BottleNumber6`'s rule for deriving its string representation differs from that of other bottle numbers, and
2. `BottleNumber6` has the same quantity and container as its superclass.

### Prying Open The Factory

We can make the factory open for extension by meta programing in the call for the bottle class:

```ruby
class BottleNumber
  def self.for(number)
    begin
      const_get("BottleNumber#{number}")
    rescue NameError
      BottleNumber
    end.new(number)
  # ...
end
```

There are pros in that this finally makes the code open for extension, but there are certainly a list of cons: harder to read, bottle classes no longer explicitly referenced, using exceptions for flow control, and conventions for naming classes must be followed exactly

Is it worth it?
