# Chapter 5 - Reducing Costs with Duck Typing

> **Duck Types** are public interfaces that are not tied to any specific class. They replace costly dependencies on class with more forgiving dependencies on messages.

> If an object quacks like a duck and walks like a duck, then its class is immaterial, it's a duck.

## Duck Typing Mechanic
* When a new TripCoordinator and a new Driver are added, then Trip's prepare method becomes unwieldly.
	- Adding a case statement that switches on class solves the problem of sending the correct message to the correct object but causes an explosion of dependencies.
	- The number of dependencies in the *prepare* method grows.
	- This type of code propogates itself. When another new trip preparer appears, you, or the next person down the programming line, will add a new branch to the switch.
	- This is most easily demonstrated with Java enums that encapsulate behavior. The switch statement to define the behavior for each enum becomees impossible to manage.
* The refactor is shown in the way the list of things is named, **_PREPARERS_**. Preparers prepare trips!
	- Preparer becomes an abstract concept. Because it is abstract, it will change less often and becomes a safe dependency inside Trip.
	- Preparer is a public interface which is implemented by each type of preparer (Mechanic, TripCoordinator, Driver...)
	- In Ruby the interface is not strictly inforced, in Java they should be implemented by concrete classes by composition.
* Defining a method by its behavior is the first step. When a second concrete implementation is introduced, try to find the duck.
	- In Java, be wary of using abstract classes to define behavior in this way.
	> The ability to tolerate ambiguity about the class of an object is the hallmark of a confident designer. Once you begin to treat your objects as if they are defined by their behavior rather than by their class, you enter into a new realm of expressive flexible design.

## Recognizing Hidden Ducks
Replace the following with ducks!
- Case statements that switch on class / behavioral enum
- kind_of? and is_a? / instanceof
- responds_to?

> Use of kind_of?, is_a?, responds_to?, and case statements that switch on your classes indicate the presence of an unidentified duck. In each case the code is effectively saying “I know who you are and because of that *I know what you do*.” This knowledge exposes a lack of trust in collaborating objects and acts as a millstone around your object’s neck. It introduces dependencies that make code difficult to change.

> When you create duck types you must both document and test their public inter- faces. Fortunately, good tests are the best documentation, so you are already halfway done; you need only write the tests.
