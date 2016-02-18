# Chapter 4 - Creating Flexible Interfaces

> _Design deals not only with what objects know (their responsibilites) and who they know (their dependencies), but how they talk to one another. The conversation between objects takes place using their **interfaces**._

## Public Interfaces
- Reveal a class's primary responsibility.
- Are expected to be invoked by others.
- Will not change on a whim.
- Are safe for others to depend on.
- Are thoroughly documented in tests.

*When the implementation changes (think refactor), the existings tests act as a regression suite.*

## Private Interfaces
- Handle implementation details.
- Are not expected to be sent by other objects.
- Can change for any reason whatsoever.
- Are unsafe for others  to depend on.
- May not even be referenced in the tests.

*When the implementation changes (think refactor), then any "partial mocks" of the object cause your existing test suite to break, and you have lost the value of your test suitef.*

* Public methods should read like a description of responsibilities. The public interface is a contract that articulates the responsibilities of your class.
* Domain objects are easy to find but they are not at the design center of your application. Instead, they are a trap for the unwary. If you fixate on domain objects you will tend to coerce behavior into them.

### Defining an application to find bike trips
1. Define the message (suitable_trips) and it's parameters (on_date, of_difficulty, need_bike), not the objects and their "needed" fields.
2. Define who's responsibility it is to coordinate trip finding with bicycle renting.
	> *Notice that the design conversation has been inverted. Instead of emphasising classes and what data they held, the conversation has changed. Now it revolves around messages. A public and private API are growing organically as needed.*
3. Realize that seperating concerns between trip and bicycle puts the burden on the customer to coordinate the two.
4. Converge collaboration for the customer's specific query (trips w/ bikes) into Trip Finder.

### Defining an application to prepare bikes for trips
1. I know what I want and I know how you do it 
	- For each bicycle, tell mechanic to prepare tires, brakes...
2. I know what I want and I know what you do.
	- Tell mechanic to prepare bicycles.
3. I know what I want and *I trust you to do your part.*
	- Tell mechanic to prepare trip, passing self.
	- Allows future growth to have multiple prepare trip operators, maybe one for bicycles, one for customer's, one for terrain checks.

## Create Explicit Interfaces
* Methods in a public interface should:
	- Be more *what* than *how*.
	- Have namesss that, insofar as you can anticipate, will not change.
	- Take a hash as an options parameter.
* create public methods that allow senders to get what they want without knowing how your class implements its behavior.
* Wrap ill defined public interfaces for your own personal use.

## Law of Demeter
* Restrict the number of objects to which you are sending messages.
* Don't just count dots. Don't delegate just to follow the law while ignoring its spirit.
* Tell your object to do something, removing the implementation deatils of how it happens, and what other objects take the specific actions.