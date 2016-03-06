# Chapter 2 - Working with Feedback
> Changes in a system can be made in two primary ways. I like to call them Edit and Pray and Cover and Modify.
> Testing should not be soley done at the application level. The feedback loop is too slow. Small localized tests are invaluable for speeding up the development cycle.

## Problems with large tests
- **Error Localization** - As tests get further from what they test, it is harder to determine what a test failure means. Often it takes considerable work to pinpoint the source of a test failure.
- **Execution Time** - Larger tests tend to take longer to execute, which makes running tests frustrating.
- **Coverage** - It is hard to see the connection between a piece of code and the values that exercise it. Tests to cover new functionality might do considerable setup work for functionality unrelated to the change.

#### It's hard to believe that this book is 12 years old, but these testing issues are still being rediscovered by "prophets" like they are new revelations. Our industry is so young that it should be hard to forget the past and even harder to NOT learn from it. Why do principles like this still feel so niche?

## Qualities of good unit tests
1. They run fast
 - A unit test that takes **1/10th** of a second to run is a slow unit test.
 - An integration test might seem to be fast by itself, but when others like it are added, your test suite becomes too slow to run regularly.
 - A test is not a unit test if:
   - It talks to a database.
   - It communicates across a network.
   - It touches the file system.
   - You have to do special things to your environment (such as editing configuration files) to run it.
2. They help us localize problems.
 - If a test fails it's immediately obvious where the broken functionality lives.
 - When changing functionality, it's clear where to define the new functionality by updating the test.

## Purposes of higher-level tests
- Pin down behavior of a group of classes for easier refactoring.

### Goal
Make functional changes that deliver value while bringing more of the system under test.

### Process
1. Identify change points.
2. Find test points.
3. Break dependencies.
4. Write tests.
5. Make changes and refactor.
