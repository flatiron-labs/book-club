## Chapter 9 - Developing (Part 1)


### Summary

Chapter 9 is focused on development practices that can be adopted to improve the quality of code and make good use of the entire team (customers, programmers, testers, etc.) The four we will cover are:
 
 Practice | Tagline    | Audience
 ---------|------------|---------
 Incremental Requirements| We define requirements in parallel with other work. | Customers
 Customer Tests | We implement tricky domain concepts correctly. | Everyone
 Test-Driven Development | We produce well-design, well-testsed, and well-factored code in small, verifiable steps. | Programmers
 Refactoring | Every day, our code is slightly better than it was the day before. | Programmers

### Some possible questions for discussion

1. "The best way I know to reduce the cost of writing software is to improve the internal quality of its code and design. I've **never** seen high quality on a well-managed project fail to repay its investment. It **always** reduces the cost of development in the short term as well as the long term." How does this fit with your experience?
1. What are each of these practices, and how do they lead to higher internal quality? Which of these are we doing here at Flatiron?
1. Who is/are the customers for Learn? How do we communicate with them.
1. This reading identifies four different types of test. What are they? What do we do at Flatiron? How's that working out?
	* Customer tests (282)
	* Unit tests (302)
	* Focused Integration Tests (303)
	* End-to-End Tests (304)
1. The reading identifies a number of "Code Smells". What are they, and which ones (if any) do you encounter here? 
	* Divergent Change and Shotgun Surgery
	* Primitive Obsession and Data Clumps
	* Data Class and Wannabe Static Class
	* Coding Nulls
	* Time Dependencies and Half-Baked Objects
1. Refactoring is cool, how do you know when to do it? How do you know when to stop?


### Themes

Here are some of the recurring themes that I noticed within these four sections. I'm just listing them here without much comment, but rather to help squeeze your mind-grapes.

* Try to produce stuff just-in-time.
* Use the roughest approximation that will work.
* Cross functionality is better than using handoffs.
* On-site Customer, please please please have one.
* Building empathy/understanding is long-term goal.
* Try to express intent, whether customer or programmer, in code.
* "Business rules" are a thing separate from "requirements"
* Small increments, whenever you can.
* Develop an oral culture as opposed to a written culture.
* Optimize for fast feedback.
* Sometimes, turn a process around to get better results (test first, design retroactively).


### Table of Contents

* Developing
	* Incremental Requirements
		* The Living Requirements Document
		* Work Incrementally
			* Vision, features, and stories
			* Rough expectations
			* Mock-ups, customer tests, and completion criteria
			* Customer review
	* Customer Tests
		* Describe
		* Demonstrate
		* Develop
		* Focus on Business Rules
		* Ask Customers to Lead
		* Automating the Examples
	* Test-Driven Development
		* Why TDD Works
		* How to Use TDD
			* Step 1: Think
			* Step 2: Red bar
			* Step 3: Green bar
			* Step 4: Refactor
			* Step 5: Repeat
		* A TDD Example
		* Testing Tools
		* Speed Matters
		* Unit Tests
		* Focused Integration Tests
		* End-To-End Tests
		* TDD and Legacy Code
	* Refactoring
		* Reflective Design
			* Divergent Change and Shotgun Surgery
			* Primitive Obsession and Data Clumps
			* Data Class and Wannabe Static Class
			* Coding Nulls
			* Time Dependencies and Half-Baked Objects
		* Analyzing Existing Code
		* How to Refactor
		* Refactoring in Action
