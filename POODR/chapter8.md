# Chapter 8 - Combining Objects with Composition

> Composition is the act of combining distinct parts into a complex whole such that the whole becomes more than the sum of its parts.

## Refactoring into Composition

### Delegating to Parts
1. Identify that Parts belonging to a Bicycle should know whether and what spares they need, not the Bicycle.
2. Create Parts object to hold parts behavior.
3. Provide Bicycle with Parts and delegate spares message to parts.
4. Extract a Parts Heirarchy for "bike kits".
**Not much of an improvement.**
*Realize that bicycles hierarchy only exists to support parts kits.*

### Composing the Parts Object
1. Create a Part object.
2. Update Parts to hold a collection of Parts.
3. Parts will be created containing a list of objects that respond to the Part interface.
**Parts only responsds to spares, but resembles an array.**
*Part holds specific knowledge about whether it is required as a spare.*

### Making Parts Work More Like an Array
1. Naive solution is to add size method to Parts. Many other methods are still missing, though.
2. Slightly less Naive is to have parts extend Array. Array methods, unfortunately, return Array, though.
3. Forawrd iterative methods to Enumerable. Slightly complex, but accomplishes desired behavior.
**Instances of bicycle needs to be instantiated with knowledge of its parts kit.**
*Parts responds to all enumerable methods.*

### Instantiating Part Objects
1. Create a config 2D array of Part configurations.
2. Create a new PartsFactory which accepts a config and creates a Parts object.
3. Now that PartsFactory exists, Part can be transformed into an OpenStruct contained within PartsFactory.
**configuration has been pushed into a datastructure.**
*Types of Bicycle of have refactored out.*
*New Bicycle instances are created by simply defining a list of parts.*



## Deciding Between Inheritance and Composition

> As a general rule, favor Composition. It contains fewer dependencies than inheritance. Inheritance, however, is a better solution when its use provides high rewards for low risk.

### Benefits of Inheritance
- Heirarchies are *reasonable*. Big changes in behavior can be achieved via small changes in code.
- Heirarchies are *open-closed*, and thus, *usable*. It's easy to create new sub classes.
- Heirarchies are *exemplary* by their ability to easily create new concrete implementations.

### Costs of Inheritance
- Inheritance is **HARD** to get right.
- Designing inheritance up front is an easy trap for solving the wrong problem.
- Inheritance is often confused as being the best way to remove duplicate code.
- Large inheritance structures are difficult to change and result in duplicated code and concepts, exactly the issue inheritance originaly tried to prevent.
- Inheritance often creates concrete instances that do not implement all functionality of its entire family tree.
- Changes at the top of the inheritance tree are very high cost.
- It is difficult to define a concrete instance that mixes behavior of multiple parents. i.e. RecumbentMountainBike.

> Biggest question when considering inheritance: "What will happen *when* I'm wrong?"
> Avoid writing frameworks that require users of your code to subclass your objects in order to gain your behavior. Their application's objects may already be arranged in a heirarchy; inheriting from your framework may not be possible.


### Benefits of Composition
- Small objects have a *single responsibility* and are *transparent*.
- It's easy to understand the code, and what will happen when you make changes.
- Adding new behavior or a new type is *reasonable*, accombplished by simply plugging in a new object.
- Objects that participate in composition are small, structurally independent, and have well-defined interfaces.

### Costs of Composition
- Composed objects rely on many parts, meaning that with size, the combined behavior of the whole is less obvious.
- Automatic message delegation is lost, and composed objects must know which messages to delete and to whom.
- Identical delegation code may be needed by many different objects.
- Clearly identifies shared behavior and structure that can be refactored out by inheritance.

## Choosing Relationships
* "Inheritance is specialization." -Bertrand Meyer, Touch of Class: Learning to Program Well with Objects and Contracts* "Inheritance is best suited to adding functionally to existing classes when you will use most of the old code and add relatively small amounts of new code." -Erich Gamma, Richard Helm, Ralph Johnson, and John Vlissides, Design Patterns: Elements of Reusable Object-Oriented Software* "Use composition when the behavior is more than the sum of its parts." -para-phrase of Grady Booch, Object-Oriented Analysis and Design

* __Inheritance__ for _is-a_ relationships
* __Duck Typing__ for _behaves-like-a_ relationships
* __Composition__ for _has-a_ relationships



#### P.S
> *Composition* involves objects that do not have a life independent of its container.
> *Aggregation* is composition where contained objects have an independent life.


