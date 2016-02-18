# Chapter 7 - Sharing Role Behavior with Modules

## Roles
> Common behavior is often orthogonal to a class; it's a *role* an object plays.

> When a role needs shared behavior, you're faced with the problem of organizing the shared code. Ideally this code would be defined in a single place but be usabe by any object that wished to act as the duck type and play the role.

## Organizing Responsibilities
1. Creating schedulable? with the most naive solution creates a switch on object type to determine lead_time, then added its own algorithm based on the lead_time to determine schedulability.
	- This creates too many dependencies in Schedule and moves responsibility away from the objects being scheduled.
2. lead_days is then moved down into the objects being scheduled, creating a duck type.
	- Dependencies are removed from Schedule
	- Unfortunately there is still a tight coupling between Schedule and the object. You must communicate through the schedule to determine whether an object is schedulable.
	- The objects should speak for themselves about whether they are schedulable.
3. schedulable? becomes behavior that is owned by an object
	1. The implementation of schedulable? is pushed into an arbitrary concrete class (Bicycle)
	2. Schedule becomes a dependency on Bicycle, who know can answer for itself when asked if it is scheduled? or schedulable?. It uses Schedule to anser these questions, which is a more appropriate dependency direction.
3. To be shared the behavior is moved up into a module that can be mixed into Schedulable objects.
	1. The module Schedulable is created
		- Holds the dependency on Schedule
		- Defines shared behavior schedulable? and scheduled?
		- Defines the algorithm for interacting with schedule on behalf of the object that is schedulable	
		- Defines a default implementation for the lead days of a schedulable object
	2. Bicycle now includes the Schedulable behavior as a mix in
	3. Dependencies are removed from the concrete class, which now only has the responsibility of providing its lead_days if they differ from the default
		- **This is the D in SOLID. Dependency Inversion Principle (DIP). The concrete class Bicycle depends on the abstract Schedulable**
	4. Schedulable contains shared code that can be used by any schedulable object.
	
### The main difference between mixins and classical inheritance becomes a discussion about whether an object *is-a* or *behaves-like-a*



### A nice illustration of the law of demeter that is violated in Java
> It’s easiest to illustrate these dependencies with an extreme example. Imagine a StringUtils class that implements utility methods for managing strings. You can ask StringUtils if a string is empty by sending StringUtils.empty?(some_string).If you have written much object-oriented code you will find this idea ridiculous. Using a separate class to manage strings is patently redundant; strings are objects, they have their own behavior, they manage themselves. Requiring that other objects know about a third party, StringUtils, to get behavior from a string complicates the code by adding an unnecessary dependency.
## Writing Inheritable Code- Code that checks the type to determine which message to send  - Within the class: Typically means that there is shared behavior that can be moved up and into a superclass
  - By the caller: Typically means there is a duck type interface that needs to be estabilished
-  Duck types often share behavior which can be moved into a mixin
- None of the code in a superclass should be specific to any implementation. The sympom are subclasses that implement a method and raise a "does not impement"
- Do not pre-optomize for abstraction, let it grow naturally from the desire to remvoe duplicate code and behavior from related objects
- Subclasses agree to a *contract*; they promise to be substitutable for their superclasses... They are not permitted to do anything that forces others to check their type in order to know how to treat them or what the expect of them.
	- This is the L is SOLID. Liskov Substitution Priciple (LSP). In order for you abstraction to be valid, your specific implementation should be substitutable with any other implemenation (ex: ArrayList vs LinkedList)
- Use the template method pattern to define inheritable code.
- Avoid writing code that requires its inheritors to send super; instead, invert the dependency and provide a hook for subclasses to implement.
- Favor shallow hierarchies.