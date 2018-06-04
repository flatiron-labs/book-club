# Chapter 5 Separating Responsibilities

Code: https://github.com/talum/99bottles/commit/3120ccc3aa7d7227bc6fb1513bc770e4652aeb5d

Summary: "This chapter explores what it means to model abstractions and rely on messages; it considers the consequences of mutation and the perils of premature performance optimization." Sandi Metz, Katrina Owen. 99 Bottles of OOP (Kindle Locations 5107-5108). 

On refactoring and chapter 4 changes: "The truth about refactoring is that it sometimes makes things worse, in which case your efforts serve gallantly to disprove an idea." Sandi Metz, Katrina Owen. 99 Bottles of OOP (Kindle Locations 5096-5097). 

# 5.1 Code Smell

## Patterns / Common Qualities
"Superfluous difference raises the cost of reading code, and increases the difficulty of future refactorings." Sandi Metz, Katrina Owen. 99 Bottles of OOP (Kindle Location 5247). 
- Q: Do we need a Ruby style guide? Or do we just need to be more cognizant of these potential variations?

## Squint Test
"Changes in color indicate differences in the level of abstraction. A method that intermixes many colors tells a story that will be difficult to follow." Sandi Metz, Katrina Owen. 99 Bottles of OOP (Kindle Locations 5259-5260).
- Q: Can anyone elaborate on this? Give an example?

## Q3: Arguments of the same name mean the same thing?
"Do arguments of the same name always mean the same thing?" Sandi Metz, Katrina Owen. 99 Bottles of OOP (Kindle Location 5278). 
- Verse number vs. number of bottles
- Q: "Having multiple methods that take the same argument is a code smell." - Sandi Metz, Katrina Owen. 99 Bottles of OOP (Kindle Locations 5376-5377). Agree or disagree? Why?

## On Conditionals
Premise: Conditionals indicate that objects are missing
Counterpoint: "This is not to say that you’ll never have a conditional in an object-oriented application. There is a place for conditionals in OO. Manageable OO applications consist of pools of small objects that collaborate to accomplish tasks. Collaborators must be brought together in useful combinations, and assembling these combinations requires knowing which objects are suitable. Some object, somewhere, must choose which objects to create, and this often involves a conditional." Sandi Metz, Katrina Owen. 99 Bottles of OOP (Kindle Locations 5484-5487). 

# 5.2 Extracting Classes
## Primitive Obsession
"Primitive Obsession is when you use one of these data classes to represent a concept in your domain. Obsessing on a primitive results in code that passes built-in types around, and supplies behavior for them." Sandi Metz, Katrina Owen. 99 Bottles of OOP (Kindle Locations 5506-5507). 

## Naming Classes
- `BottleNumber`: "The rule about naming can thus be amended: while you should continue to name methods after what they mean, classes can be named after what they are." Sandi Metz, Katrina Owen. 99 Bottles of OOP (Kindle Locations 5547-5548). 

## Extraction Process
- Copy everything
- Forward messages
- Remove old stuff
  - Change argument name and provide default
  - Change very sender of message
  - Delete argument
  
# 5.3 Appreciating Immutability
- Immutable objects are easy to understand, reason about, and test
- Q: Make more objects that don't change (y/n)?

# 5.4 Assuming Fast Enough
- Cache invalidation is hard and we're bad at predicting when to invalidate a cache
- Write the simplest code possible and measure after 
- Avoid caching, use immutable objects, treat object creation as free
  - Addendum: Don't do complex DB queries in the initialize method
- "Your goal is to optimize for ease of understanding while maintaining performance that’s fast enough. Don’t sacrifice readability in advance of having solid performance data." Sandi Metz, Katrina Owen. 99 Bottles of OOP (Kindle Locations 6262-6263). 

# 5.5 Creating Bottle Numbers
- "BottleNumber s implement successor, and it feels as if successor should return the object you need." Sandi Metz, Katrina Owen. 99 Bottles of OOP (Kindle Locations 6483-6485). 
- kinda feels like a logical leap, but sure...
