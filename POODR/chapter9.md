# Chapter 9 - Designing Cost Effective Tests

> Well-designed code is easy to change, refactoring is how you change from one design to the next, and tests free you to refactor with impunity.

## Intentional Testing
> The true purpose of testing, just like the true purpose of design, is to reduce costs... [and improve confidence]

- **Finding Bugs**
- **Supplying Documentation**
- **Deferring Design Decisions**
	Allows you to code to an interface but have concrete / incomplete decisions underneath. When refactoring, your interface protects you.
- **Exposing Design Flaws**
	- If a test requires painful setup, the code expects too much context.
	- If testing one objects drags a bunch of others into the mix, the code has too many dependencies.
	- If a test is hard to write, other objects will find the code difficult to reuse.
	
	
## Knowing What to Test
- Your goal is to write loosly coupled tests about only the things that matter... The safest way to accomplish this is to test everything just once and in the proper place.
- The tests you write should be for messages that are defined in public interfaces. The most costly and least useful tests are those that blast holes in an object's containment walls by coupling to unstable internal details.
- An object should not test the state of messages to collaborating objects.
- A test should not test any private apis of the object under test.

## Types  of Tests
- *Incoming* messages are your public interface. They need to be tested for the state they return.
- *Query* messages have no side effects. Their contents don't necessarily need to be sent. You will likely prove their contents are properly recieved through stubbing the response.
- *Command* messages do have side effects. Their contents should be verified. Proving that their message gets sent properly is a test of behavior, and not state.

> Writing tests first forces a modicum of reusability to be built into an object from its inception. It would otherwise be impossible to write tests at all. Novice designers are best service by TDD.
> Don’t overestimate your strengths and use an inflated self-view as an excuse to avoid tests. While it some- times makes sense to write a bit of code the old fashioned way, you should err on the side of test-first.

## Testing Incoming Messages

### Do not test an incoming message that has no dependents; delete it.
> What purpose is served by implementing a message that no one sends? It’s not really incoming at all, it’s a speculative implementation that reeks of guessing about the future and clearly anticipates requirements that do not exist.

### Incoming messages are tested by making assertions about the value, or state, that their invocation returns; proving that they return the correct value in every possible situation.
- If a dependency of the object under test is expensive to create, then coupling the test to that dependency will slow down your tests.
- If a dependency of the object under test changes, then the test incurrs unintended consequences.
- When tightly coupled objects are tested, a test of one object runs code in many others.

### Using Doubles
- Using a real Wheel to test Gear means that an update to the public interface of Wheel causes the Gear test to fail in an expected manner.
- Using a double to stub the response of a Diameterizable object decouples the Gear test from a concrete and possibly expensive dependency.
- Using a double to stub the response will mean that the same change to the public interface of Wheel allows the test suite to stay green while the code fails at runtime. The value of the test has been lost.

### Testing Private Methods
- Testing private methods is redundent as their functionality is covered by tests of public methods using the private method.
- Private methods are unstable meaning that the tests are tightly coupled and likely to change.
- Testing private methods can mislead others into using them as Tests provide documentation about the object under test.
- The rules-of-thumb for testing private methods are thus: *Never write them, and if you do, never ever test them.* This bias can be broken with intention, but doing so should be thoughtful activity.

### Testing Outgoing Messages
- Using a real Observer when verifying that Gear has changed means that the message sent to Observer is never explicitly tested. There's no guarentee that Gear follows the contract. 
- Using a real Observer makes it difficult to verify the side effects that occur as a result of the action.
- Using a real Observer results in duplicated test coverage of objects not directly under test, meaning that changes in those classes break the tightly coupled tests for the wrong object.
- Mocking the dependency Observer provides a way to verify that Gear behaves correctly and sends the appropriate message.
- Mocking the dependency allows you to verify that side effects are properly triggered by the object under test.

### Testing Duck Types
- Create a module which defines a test to validate that the object adheres to the interface.
- Include the module in each test for concrete implementations that implement the interface.
- Including the module in the concrete implementation also serves as documentation about the functionality of the object being tested.
- Including the module in the test relying on the functionality ensures that the test utilizing the stubbed interface will fail if the interface changes.
- In Java, this is accomplished by defining a shared interface. The compiler runs the test for you to ensure that each concrete implementation correctly implements the interface.

### Testing Inherited Code
- Define a shared module that tests the contract. This ensures that LSP is adhered to. It will also signal to errors in the heirarchical abstraction. Include this module in the test of each subclass.
- Define a shared module that tests the required bevavior of each subclass. This ensures that each subclass responds to messages required by the superclass. Include this module in the test of each subclass.
- These test modules give confidence that each subclass follows its contract.
- They also provide programmers new to that area of the code documentation about the heirarchy.
- After inheriting testing modules, subclasses should only test specialized behavior. Testing shared behavior is redundant and produces fragile tests.
- A stubbed instance of the abstract class should be created for the purpose of testing the shared functionality provided by the abstract class.
- Be sure to include the SubclassTestModule to test the contract of the stubbed abstract class.