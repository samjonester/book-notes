# Chapter 9 - I Can't Get This Class into a Test Harness

The four most common problems encountered
1. Objects of the class can't be created easily.
2. The test harness won't easily build with the class in it.
3. The constructor we need to use has bad side effects.
4. Significant work happens in the constructor, and we need to sense it.

## Provided dependencies
- Dependencies that are provided to an object through its constructor.
- Pass fakes into constructors that accept dependencies.

> CreditValidator validator = new CreditValidator(connection, null, "a");
>
> The way people react to lines of code like that often says a lot about the kind of system they work on. If you looked at it and said, "Oh, fine, so he’s passing a null into the constructor—we do that all the time in our system," chances are, you’ve got a pretty nasty system on your hands. You probably have checks for null all over the place and a lot of conditional code that you use to figure out what you have and what you can do with it.

Tests should provide documentation for proper interactions with an object. Passing null into the class encourages more of that bad behavior. Use a mock instead.

## Null object pattern
Avoid providing null! Provide a safe instance of the object instead. This is the case for monads.

## Hidden dependencies
- Dependencies that are created by the class under test.
- **Parameterize** the dependencies so that they can be faked as well.
- Create a second constructor that accepts the dependencies for testing.
- The original will instantiate it's dependencies and call the new constructor.

## Constructor Blob
- Constructor instantiates many objects, using one to instantiate the next.
- Use a *supersede setter* to provide your own implementation.
- Create a setter that updates the object's dependency.
- After constructing the object, call this setter with a fake.

## Global Dependencies
- These include **static method calls** and **singletons**.
- Sometimes these are so pervasive in a code base that parameterizing them isn't possible.
- One possibility is to provide a static method for updating the singleton to provide it testing information, but that will most likely cause us to instantiate the singleton. This is in conflict with why the singleton was created.

Why do we desire to have one and only one instance?  
  1. **We are modeling the real world, and there is only one of these things in the real world.**
  2. **If two of these things are created, we could have a serious problem.**
  3. **If someone creates two of these things, we’ll be using too many resources.**
  4. **You want a global variable, and it would be too painful to pass the variable around to the places where it is needed.**  
All of these reasons smell of a larger design problem and a poor testing environment.
