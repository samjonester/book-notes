# Forward
> Sometimes we blame our customers. Sometimes we accuse them of changing the requirements. We comfort ourselves with the belief that if the customers had just been happy with what they said they needed, the design would have been fine. It's the customer's fault for changing the requirements on us.
> Well, here's a news flash: *__Requirements change.__ Designs that cannot tolerate changing requirements are poor designs to begin with.* It is the goal of every competent software developer to create designs that tolerate change.

# Preface
> Legacy code is untested code.
- I suppose that makes sense, as tests influence a better design, but I've seen tested code that is inflexible. I've also seen code that is "tested" at a high level but not thoroughly bear the marks of complexity and tight coupling.
> Good design should be a goal for all of us, but in legacy code, it is something that we arrive at in discrete steps.
> We are trying to get to a point which we are used to ease; we expect it and actively attempt to make code change easier.
> "Before I'd arrived, they'd realized that unit testing was a great thing, but the tests that they were executing were full scenario tests that made multiple trips to a database and exercised large chunks of code. The tests were hard to write, and the team didn't run them very often because they took so long to run."

# Chapter 1 - Changing Software

## Adding Features and Fixing Bugs
Both fixing bugs and adding features are changing code. There is, however a big difference between behaviors of change. Are we *Adding*, *Changing*, or *Removing* behavior, or is it a combination of changes.

## Improving Design
Altering software's structure to make it more maintainable, often called *Refactoring*. Generally we want to keep its behavior intact. We often call removed behavior in this situation a bug.

## Optimization
Refactoring with a different goal, to improve performance or memory usage.

|                   | Adding a Feature | Fixing a Bug | Refactoring | Optimizing |
|-------------------|------------------|--------------|-------------|------------|
| Structure         | Changes          | Changes      | Changes     |     --     |
| New Functionality | Changes          |  --          | --          |     --     |
| Functionality     | --               | Changes      | --          |     --     |
| Resource Usage    | --               |  --          | --          | Changes    |

## Anti-patterns
- "If it's not broke, don't fix it."
- "What? Create another method for that? No, I'll just put the lines of code right here in the method, where I can see them and the rest of the code. It involves less editing, and it's safer."

> It's tempting to think that we can minimize software problems by avoiding them, but unfortunately, it always catches up with us. When we avoid creating new classes and methods, the existing ones grow larger and harder to understand.
> Avoiding change has other bad consequences. When people don't make changes often they get rusty at it. Breaking down a big class into pieces can be pretty involved work unless you do it a couple of times a week.

