# Chapter 6 - Acquiring Behavior Through Inheritance

> Inheritance is, at its core, a mechanism for automatic message *delegation*. It defines a forwarding path for not-understood messages.

##Abstraction Path
1. Start with concrete Class to let abstraction grow organically, **trusting** the next developer to do the refactor.
2. If the second concrete implementation is added to the existing class, then new logical branching based on type is created.
	- Stopping here leaks state and will pollute your code base.
	- Interface / abstraction could remove conditionals.
	- Variables with the names **_Type, Category, Style..._** are cues to take notice of the underlying pattern
4. Find generalized ideas that can be abstracted. Be careful to not leave any specific knowledge in the generalized superclass.
5. After generalizing into an *abstract class*, the Bicycle class should no longer be instantiated and used seperately.
6. Avoid abstracting until a clear pattern of abstraction has emerged organically. **DO NOT** create an abstract class first!
7. When using the *template method pattern (i.e. abstract methods)* be sure that the superclass implements the method itself. If no default implementation can be provided, then raise a descriptive NotImplementedError
	raise NotImplementedError, "This #{self.class} cannot responsd to:"
8. Requiring subclasses to know about and call super methods presents duplicated behavior in subclasses. It tightly couples the superclasses and subclasses together, and adds unnecessary work and knowledge needed by future implementers. **It adds _dependency_ on the knowledge of super's algorithm.**
9. The superclass should instead call a method that is optionally implemented by subclasses. This retains control of the algorithm in the superclass, drying up the duplicated behavior from the subclasses. Future implementers then only implement the methods which make it specific from its parent.

> Poor class heirarchies for objects that interact with them to know their quirks, and these quirks become embeded in other code.