# Chapter 10 - I Can't Run This Method in a Test Harness

> Instantiating a class is often only the first part of the battle. The second part is writing tests for the methods we need to change.

- Method might not be accessible to the test. It could be private or have some other accessibility problem.
- It might be hard to call the method because it is hard to construct the parameters we need to call it.
- The method might have bad side effects (modifying a database, launching a cruise missile, and so on), so it is impossible to run in a test harness.
- We might need to sense through some object that the method uses.

## Method size
If the method size is a problem and causing data setup to be difficult. Extract methods from pieces of work. This will also help better document the intent of each piece of work within a large method. Then move those units of work into their own classes. Eventually, you'll be left with a delegating method whose complicated logic has been pushed down into testable units.

## Hidden Methods
1. If possible, test through it's public entry point. This will at least help with refactoring the method into a more manageable state.
2. Consider making the method public. This will help us identify the smell in the design that causes us to desire to test a private method.
  - It could mean that the class is too large and doing too much.
  - It causes bad side effects for its enclosing class, and is not a pure function.
  - It is just a utility used by this one class that callers shouldn't need to know about.
3. If the method cannot reasonably be part of the classes public api, then it should be moved into its own class and tested in isolation. Side effects should be examined carefully; attempt to remove them.

## Undetectable Side Effect
When side effects happen that are not the obvious when calling the method, break the dependency and fake the interaction with the side effect producing code. Verify that the side effect was triggered and your test will become documentation that it's happening.

## Command / Query Separation
*A method should be a command or a query, but not both.*
A command is a method that can modify the state of the object but that doesn't return a value. A query is a method that returns a value but that does not modify the object.
This is important to communicate intent.
