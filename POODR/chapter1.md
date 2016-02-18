# Chapter 1 - Object-Oriented Design

### Change happens and is hard
> "Applications that are easy to change are a pleasure to write and a joy to extend. They're flexiby and adaptable. Applications that resist chagne are just the opposite; every change is expensive and each makes the next cost more."

> "When objects know too much they have many expectations about the world in which they reside... The objects resiste being reused in difference contexts; they are painful to test and susceptible to being duplicated."

> "The future that design considers is not one in which you anticipate unknown requirements and preemptively choose one from among the m to implement in the present... Practical design does not anticipate what will happen to your application, it merely accepts that something will... it preserves your options for accommodating the future."

### Tools of design
* **S** - Single responsibility - Only do one thing
* **O** - Open-Closed - Open for extension, closed for modification
* **L** - Liskov Substitution - Subclasses should be able to be swapped without affecting code. less neive inheritance model.
* **I** - Interface Segregation - Client's shouldn't be forced to rely on interfaces they don't explicitly use. No no-op methods because you implemented an interface. That should probably be split into multiple interfaces.
* **D** - Dependency Inversion -  High-level modules should not depend on low-level modules. Both should depend on abstractions. Don't build a pyramid, where high level abstractions rely on the implementatin of lower levels.
* 
* **DRY** - Don't Repeat Yourself. Not specific to code duplication, can be more powerful when examining behaviors and concepts.
* **Law of Demeter** - Limit knowledge of other collaborators to only what is necessary.


- **Controversial Discussion Point:**
"Pattern misapplicaiton results in complicated and confusing code but this result is not the fault of the pattern itself. A tool cannot be faulted for its use, the user must master the tool."
 * Shah - "This arguement can be used to justify the use of the wrong tool."
 * I feel that using the wrong tool means that you have not mastered it. You wouldn't call yourself a master with a spatula if you're using it to slice bread."

### How design fails
**Stages**
- Beginner: Design fails due to lack of it. Result: Code becomes overly comples and imposible to change. "Yes, I can add that feature, *but it will break everything*."
- Intermediate: Do not fully understand OO design, and with the best intentions fall into the trap of overdesign. Result: Code becomes  castle, hemming them in with stone walls. "No, I can't add that feature; *it wasn't designed to do that*."

I have seen both stages in myself and my code, and the reason why I am reading this book is to begin to move past it. I am sharing this book and organizing this group so that others can learn with me. It may sound selfish, but I don't want to be the only one trying to improve myself, because we are all strongly influenced by our environment and our peers. Also we need to rely on the code we write as a group, so it's selfish to not try to improve yourself for the benefit of everyone else in the group.

### Balancing design and delivery
**Thourough design** can easily cost much more up front.
**Under designing** can quickly cost much more in the future.
- It is hard to determine how much cutting corners will cost in the future.
- It is very hard to start slow with a deadline looming ahead.
- It is very easy to say "We'll come back to that" or "We will refactor that later" or "I just can't take the time to do it better now".
- In practice, August never comes, and that code never changes. Is it in a state that someone else can inherit it and continue to be productive? Every line of code you write **_WILL_** be read and probably modified by someone else, without the context in which you wrote it... Scary! ...humbling

### Intro to OOP
#### Procedural Programming
> "Each action is a simple script... It knows about a small, fixed set of different kinds of data, things like strings, numbers, arrays, maps"

- Grouping of functionality feels haphazard. 
- You are always asking data about itself so that you can take actions yourself. Data is stored naively in nondescript locations for later user.
- "Data is one thing, behavior is something completely different. Data gets packaged up into variables and then passed around to behavior, which could, frankly, do anything with it. Data is like a child that behavior send off to school every morning; there is no way of knowing what actually happens while it is out of sight. The influences on data can be unpredictable and largely untraceable."

#### Object-Oriented Programming
> "Instead of dividing data and behavior into two separate, never-the-twain-shall-meet spheres... objects have behavior and may contain data, data to which they alone control access. Objects invoke one another's behavior by sending each other *messages*."

- An object defines behavior and attributes. 
- An object does not hold state for procedural logic. An object is told what to do.
- An object is a thing that does something, not an action that is decuppled from its data.
