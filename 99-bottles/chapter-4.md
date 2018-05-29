## 99 Bottles Chapter 4: Practicing Horizontal Refactoring

Github commits: https://github.com/nt591/99bottles-ch4/commits/master

### Replacing	Difference	With	Sameness

The first goal for horizontal refactoring is to identify the MOST ALIKE pieces of code (aka the smallest amount of difference to change). In this case, look at the case for `1` and `else`

What are the differences? First number (1 vs number-1, bottles vs bottles/container(), take it down vs take one down.

#### First line: Number
First change to make, change to `number`


#### First line> Container
We have a dynamic `container` method from chapter 3!

#### Repeat for second line

### Names: It vs One
Strategies for naming?
- Good enough name: Some	folks	allot	themselves	five	to	ten	minutes	to	ponder	(usually	with	thesaurus	in	hand),	and	then
use	the	best	name	they	can	come	up	with	during	that	interval.	
- Meaningless name: Other	folks	find	it	more	cost	effective	to	instantly	choose	a	meaningless	name	like	 foo 	or	 namethis .
This	strategy	allows	them	to	move	forward	quickly,	and	(one	hopes)	insures	that	the	name	will	get
improved	later.	
- Name guru: Within	any	group	of	programmers,	there’s	often	someone	who’s	good	at	naming	things.	If
your	group	has	such	a	person,	you	know	who	they	are.	Appoint	them	the	"name	guru,"	and	leverage
their	strengths	when	you	need	a	name.

#### The pronoun method:

This was interesting, and I still don't feel like I understand why the default argument is needed unless you're running tests on every code change (which I guess you are?)

I would just as happily update `pronoun` to take an argument AND update all known uses of `pronoun` to pass in an argument. Discussion: How much of this is useful in real world application vs just an exercise?

#### Deriving	Names	From	Responsibilities

"what	would	the	column	header	be?" is a really intuitive technique in this case (essentially descriptors of a small return value or non-computationally hard method (container, quantity) but seems harder for other cases (`AssignedRepo#update_assigned_repo_performance_profile`)

> "quantity 	at	least	attempts	to	indicate	the	responsibility	on	the	method	you	plan	to	create,
and	so	is	a	reasonable	first	attempt	at	a	name."

I liked the "reasonable first attempt" part - I don't find myself always open to changing a method name as the information changes.

#### Choosing	Meaningful	Defaults

:FIXME fails in the `quantity` case because in the false case, we return the default. 

> "The	reason	the	 :FIXME 	default	worked	in	previous	situations	was	because	in	those	cases	you	wanted
to	execute	the	false	branch.	However,	now	you	need	the	true	branch,	and	therefore	require	a	much
more	specific	default"

#### Random notes:
I thought the flow of going line by line was interesting. I don't think when I've tried to abstract out common code, I've done it in such a structured path. I often end up looking at two pieces of code (classes, React components) and seeing some superficial similarities, pulling them out and trying to make the rest "fit"

I'm definitely going to at least use this method going forward.

> When	the	 else 	branch	is	implemented	first,	 :FIXME 	can	always	be	used	for	the	default.	This	not
only	saves	you	from	having	to	figure	out	the	right	value,	it	also	serves	as	a	reminder	to	remove	this
temporary	default	later.	

> 	If	the	non- else 	branch	is	implemented	first,	the	default	has	to	be	set	to
something	that	actually	meets	the	condition	and	so	makes	the	 true 	branch	execute.	Therefore,
implementing	the	non- else 	branch	first	places	a	slightly	greater	burden	on	you.	You	have	to	use	a
specific,	real	value	for	the	default,	and	then	remember	to	remove	the	default	once	the	transition	is
complete.

#### Seeking	Stable	Landing	Points

> Notice	the	similarities	in	the	above	methods.	Each	has	a	single	responsibility.	They	are	identical	in
shape.	All	take	the	same	argument.	Each	contains	a	conditional	and	that	conditional	tests	the	argument
against	a	specific	value;	it	checks	to	see	if	the	argument	is	equal	to	something,	as	opposed	to	greater	or
less	than	something.	

There's something useful in readability about all the methods have the same "contract" (aka they check a given value for quality and return if/else)

Discussion: How can we be better at making our private methods or helpers more consistent? What do we do when business logic dictates they AREN'T similar?

#### Obeying	the	Liskov	Substitution	Principle
https://stackoverflow.com/a/584732 is helpful

`quantity(number).capitalize` only works in the `number == 0` case because our method could return EITHER a String OR Integer

We could always call `to_s` (STRING.to_s is meaningless), and creates external dependency of understanding of the internals of that method. It's better to make sure the method ALWAYS returns the same type

> Liskov,	in	plain	terms,	requires	that	objects	be	what	they	promise	they	are.	When	using	inheritance,
you	must	be	able	to	freely	substitute	an	instance	of	a	subclass	for	an	instance	of	its	superclass.
Subclasses,	by	definition,	are	all	that	their	superclasses	are,	plus	more,	so	this	substitution	should
always	work.

> Liskov	violations	force	message	senders	to	have	knowledge	of	the	various	return	types,	and	to	either
treat	them	differently,	or	convert	them	into	something	consistent.	

I definitely do this sometimes. Here's a fake example of code I definitely have written

```
def user_phone_number(user)
  return nil if user.nil?
  user.phone_number
  end
```

#### 	Taking	Bigger	Steps

Takeaways - once you find a pattern, it's okay to take bigger jumps BUT if you get red tests, you MUST undo to green and begin working in smaller steps.

#### 	Discovering	Deeper	Abstractions

I would have changed quantity, but that breaks the similarity between all our methods. How much value is there in keeping that? I like that this example was "easy" enough to find a better solution, but how much does this apply in our case?

The idea that *the shape* of your abstraction dictactes whether it is right or wrong is an interesting one - how do we converge on a common shape?

> Having	made	these	lines	as	similar	as	possible,	it	is	now	obvious	that `99` must	represent	the	same	concept	as `number - 1`

#### 	Depending	on	Abstractions

> ...	abstractions	tell	you	where	your	code	relies
upon	an	idea.	But	to	get	this	last	benefit,	you	must	refer	to	an	abstraction	in	every	place	where	it
applies.

> The	code	above	doesn’t	want	the	 container 	of	 number-1 ;	it	wants	the	 container 	of	the	following
verse.	

This is essentially focusing on code's behavior rather than code's data, and `successor` is the only thing responsible for this logic.


> One	final	thought	before	moving	on.	Consider	this	question:	If	several	different	programmers	started
from	Shameless	Green	and	refactored	the	 verse 	method	according	to	the	Flocking	Rules,	what	would
the	resulting	code	look	like?	If	you’ve	guessed	that	everyone’s	code	would	be	identical,	excepting	the
names	used	for	the	concepts,	you’d	be	right.	This	has	enormous	value.
