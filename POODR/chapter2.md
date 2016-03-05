# Chapter 2 - Definition of Easy to Change
- Changes have no unexpected side effects.
- Small changes in requirements require correspondingly small changes in code.
- Existing code is easy to reuse.
- The easiest way to make a change is to add code that in itself is easy to change.

# Qualities of Changeable Code
- **Transparent** The consequences of change shoudl be obvious in the code that is changing and in distant code that relies upon it.
- **Reasonable** The cost of any change should be proportional to the benefits the change achieves.
- **Usable** Existing code should be usable in new and unexpected contexts.
- **Exemplary** The code itself should encourage those who change it to perpetuate these qualities.

> "Another way to hone in on what a clas is actually doing is to attemp to describe it in one sentence. If the simplest description you can devise uses the work "and," the class likely has mor ethan one responsibility. If it uses the word "or," then the class has more than one responsibility and they aren't even very related"

### SRP requires that a class be cohesive - that everything the class does be highly related to its purpose.

# Depend on behavior not data
- "dry code tolerates change because any change in behavior can be made by changing code in just one place."
- "When you expose data structure it's not long before you have references to that structure all over. The references are *leaky*. They escape encapsulation and insinuate themselves throughout the code base. They are not DRY. The knowledge of the data structure should be known in just one place."

## Refactor actions into small methods
- Has a clarifying effect on their class.
- Are easy to move to another class when responsibilities have emerged.
